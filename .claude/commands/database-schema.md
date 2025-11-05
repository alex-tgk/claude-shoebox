# Design and Generate Database Schema

You are tasked with designing and generating database schemas from requirements, including migrations, models, and documentation.

## Instructions

1. **Gather Requirements**
   - Ask about the database system (PostgreSQL, MySQL, MongoDB, etc.)
   - Understand the domain and entities
   - Identify relationships between entities
   - Determine data access patterns
   - Understand scalability requirements
   - Ask about existing schemas to integrate with
   - Determine ORM/query builder (Prisma, TypeORM, GORM, sqlx)

2. **Requirements Analysis**

   For each entity, identify:
   - Entity name and purpose
   - Attributes (fields/columns)
   - Data types
   - Constraints (NOT NULL, UNIQUE, CHECK)
   - Default values
   - Relationships (one-to-one, one-to-many, many-to-many)
   - Indexes needed for performance
   - Business rules and validations

3. **Schema Design Best Practices**

   **Normalization:**
   - Apply appropriate normalization (usually 3NF)
   - Avoid data redundancy
   - Consider denormalization for read-heavy workloads
   - Balance between normalization and performance

   **Naming Conventions:**
   - Use lowercase with underscores (snake_case)
   - Plural table names (users, posts, orders)
   - Descriptive column names
   - Consistent naming across tables
   - Prefix junction tables appropriately

   **Primary Keys:**
   - Use UUID or auto-incrementing integers
   - Consider distributed systems (UUID for multi-region)
   - Add id column to all tables
   - Never expose auto-increment IDs in URLs (use UUIDs)

   **Foreign Keys:**
   - Always use foreign key constraints
   - Define ON DELETE and ON UPDATE behavior
   - Use appropriate cascade rules
   - Index foreign key columns

   **Timestamps:**
   - Add created_at to all tables
   - Add updated_at to mutable tables
   - Consider deleted_at for soft deletes
   - Use timezone-aware timestamps

4. **Relational Database Schema (PostgreSQL/MySQL)**

   **Table Design:**
   ```sql
   -- Users table
   CREATE TABLE users (
     id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
     email VARCHAR(255) NOT NULL UNIQUE,
     username VARCHAR(50) NOT NULL UNIQUE,
     password_hash VARCHAR(255) NOT NULL,
     first_name VARCHAR(100),
     last_name VARCHAR(100),
     role VARCHAR(20) NOT NULL DEFAULT 'user',
     is_active BOOLEAN NOT NULL DEFAULT true,
     created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
     updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
     deleted_at TIMESTAMP WITH TIME ZONE,

     CONSTRAINT valid_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}$'),
     CONSTRAINT valid_role CHECK (role IN ('user', 'admin', 'moderator'))
   );

   -- Create indexes
   CREATE INDEX idx_users_email ON users(email);
   CREATE INDEX idx_users_username ON users(username);
   CREATE INDEX idx_users_created_at ON users(created_at);
   CREATE INDEX idx_users_deleted_at ON users(deleted_at) WHERE deleted_at IS NULL;
   ```

   **Relationships:**
   ```sql
   -- One-to-Many: User has many Posts
   CREATE TABLE posts (
     id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
     user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
     title VARCHAR(255) NOT NULL,
     content TEXT NOT NULL,
     status VARCHAR(20) NOT NULL DEFAULT 'draft',
     published_at TIMESTAMP WITH TIME ZONE,
     created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
     updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),

     CONSTRAINT valid_status CHECK (status IN ('draft', 'published', 'archived'))
   );

   CREATE INDEX idx_posts_user_id ON posts(user_id);
   CREATE INDEX idx_posts_status ON posts(status);
   CREATE INDEX idx_posts_published_at ON posts(published_at);

   -- Many-to-Many: Posts and Tags
   CREATE TABLE tags (
     id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
     name VARCHAR(50) NOT NULL UNIQUE,
     created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW()
   );

   CREATE TABLE posts_tags (
     post_id UUID NOT NULL REFERENCES posts(id) ON DELETE CASCADE,
     tag_id UUID NOT NULL REFERENCES tags(id) ON DELETE CASCADE,
     created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),

     PRIMARY KEY (post_id, tag_id)
   );

   CREATE INDEX idx_posts_tags_post_id ON posts_tags(post_id);
   CREATE INDEX idx_posts_tags_tag_id ON posts_tags(tag_id);
   ```

5. **Advanced Features**

   **Full-Text Search (PostgreSQL):**
   ```sql
   ALTER TABLE posts ADD COLUMN search_vector tsvector;

   CREATE INDEX idx_posts_search
   ON posts USING GIN(search_vector);

   CREATE TRIGGER posts_search_update BEFORE INSERT OR UPDATE
   ON posts FOR EACH ROW EXECUTE FUNCTION
   tsvector_update_trigger(search_vector, 'pg_catalog.english', title, content);
   ```

   **Partitioning (for large tables):**
   ```sql
   CREATE TABLE events (
     id UUID NOT NULL,
     event_type VARCHAR(50) NOT NULL,
     data JSONB,
     created_at TIMESTAMP WITH TIME ZONE NOT NULL
   ) PARTITION BY RANGE (created_at);

   CREATE TABLE events_2024_01 PARTITION OF events
   FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');
   ```

   **Enumerated Types:**
   ```sql
   CREATE TYPE user_role AS ENUM ('user', 'admin', 'moderator');
   CREATE TYPE post_status AS ENUM ('draft', 'published', 'archived');
   ```

   **JSON Columns:**
   ```sql
   ALTER TABLE users ADD COLUMN preferences JSONB;
   CREATE INDEX idx_users_preferences ON users USING GIN(preferences);
   ```

6. **MongoDB Schema Design**

   ```typescript
   // User schema
   const userSchema = {
     _id: ObjectId,
     email: { type: String, required: true, unique: true },
     username: { type: String, required: true, unique: true },
     passwordHash: { type: String, required: true },
     profile: {
       firstName: String,
       lastName: String,
       avatar: String
     },
     role: {
       type: String,
       enum: ['user', 'admin', 'moderator'],
       default: 'user'
     },
     isActive: { type: Boolean, default: true },
     createdAt: { type: Date, default: Date.now },
     updatedAt: { type: Date, default: Date.now }
   };

   // Indexes
   db.users.createIndex({ email: 1 }, { unique: true });
   db.users.createIndex({ username: 1 }, { unique: true });
   db.users.createIndex({ createdAt: -1 });

   // Embedded documents vs References
   // Embed when data is accessed together
   const postSchema = {
     _id: ObjectId,
     userId: ObjectId,  // Reference to user
     title: String,
     content: String,
     tags: [String],    // Embed simple arrays
     comments: [        // Embed subdocuments
       {
         userId: ObjectId,
         text: String,
         createdAt: Date
       }
     ],
     createdAt: Date,
     updatedAt: Date
   };
   ```

7. **ORM/ODM Models**

   **Prisma Schema:**
   ```prisma
   model User {
     id        String   @id @default(uuid())
     email     String   @unique
     username  String   @unique
     password  String
     role      Role     @default(USER)
     posts     Post[]
     createdAt DateTime @default(now())
     updatedAt DateTime @updatedAt

     @@index([email])
     @@index([username])
   }

   model Post {
     id          String   @id @default(uuid())
     title       String
     content     String   @db.Text
     status      Status   @default(DRAFT)
     userId      String
     user        User     @relation(fields: [userId], references: [id], onDelete: Cascade)
     tags        Tag[]
     publishedAt DateTime?
     createdAt   DateTime @default(now())
     updatedAt   DateTime @updatedAt

     @@index([userId])
     @@index([status])
   }

   model Tag {
     id    String @id @default(uuid())
     name  String @unique
     posts Post[]
   }

   enum Role {
     USER
     ADMIN
     MODERATOR
   }

   enum Status {
     DRAFT
     PUBLISHED
     ARCHIVED
   }
   ```

   **TypeORM Entities:**
   ```typescript
   @Entity('users')
   export class User {
     @PrimaryGeneratedColumn('uuid')
     id: string;

     @Column({ unique: true })
     email: string;

     @Column({ unique: true })
     username: string;

     @Column()
     passwordHash: string;

     @Column({ type: 'enum', enum: ['user', 'admin', 'moderator'] })
     role: string;

     @OneToMany(() => Post, post => post.user)
     posts: Post[];

     @CreateDateColumn()
     createdAt: Date;

     @UpdateDateColumn()
     updatedAt: Date;

     @Index()
     @DeleteDateColumn()
     deletedAt?: Date;
   }
   ```

8. **Migrations**

   **Create migration files:**
   - Use migration tool (Prisma Migrate, TypeORM, golang-migrate)
   - One migration per schema change
   - Write both up and down migrations
   - Name migrations descriptively with timestamps

   **PostgreSQL Migration Example:**
   ```sql
   -- migrations/001_create_users_table.up.sql
   CREATE TABLE users (
     id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
     email VARCHAR(255) NOT NULL UNIQUE,
     username VARCHAR(50) NOT NULL UNIQUE,
     created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW()
   );

   -- migrations/001_create_users_table.down.sql
   DROP TABLE IF EXISTS users;
   ```

9. **Seed Data**

   Create seed scripts for development:
   ```typescript
   // seeds/users.ts
   export async function seedUsers() {
     await prisma.user.createMany({
       data: [
         {
           email: 'admin@example.com',
           username: 'admin',
           role: 'admin'
         },
         {
           email: 'user@example.com',
           username: 'user',
           role: 'user'
         }
       ]
     });
   }
   ```

10. **Performance Optimization**

    **Indexes:**
    - Index foreign keys
    - Index columns used in WHERE, JOIN, ORDER BY
    - Use composite indexes for multi-column queries
    - Avoid over-indexing (slows writes)
    - Consider partial indexes

    **Queries:**
    - Use EXPLAIN ANALYZE to optimize queries
    - Avoid SELECT *
    - Use proper JOIN types
    - Avoid N+1 queries
    - Use pagination for large datasets
    - Consider materialized views

11. **Data Integrity**

    - Use foreign key constraints
    - Add CHECK constraints for business rules
    - Use UNIQUE constraints
    - Use NOT NULL appropriately
    - Implement database-level validation
    - Use transactions for related operations

12. **Security Considerations**

    - Never store plain text passwords
    - Use prepared statements (prevent SQL injection)
    - Implement row-level security (PostgreSQL)
    - Encrypt sensitive data at rest
    - Use separate read/write users
    - Limit database user permissions
    - Regular backups
    - Audit logging

13. **Documentation**

    Create comprehensive schema documentation:
    - Entity-Relationship Diagram (ERD)
    - Table descriptions
    - Column descriptions
    - Relationship explanations
    - Index purposes
    - Migration history
    - Seed data documentation

    **Generate ERD:**
    - Use tools like dbdiagram.io
    - Use Prisma ERD generator
    - Use SchemaSpy

14. **Testing**

    - Write tests for migrations
    - Test foreign key constraints
    - Test unique constraints
    - Test check constraints
    - Test cascade deletes
    - Test with realistic data volumes

15. **Final Deliverables**

    Provide:
    - Complete SQL schema or Prisma/TypeORM models
    - Migration files
    - Seed data scripts
    - ERD diagram
    - Schema documentation
    - Index strategy explanation
    - Performance considerations
    - Setup instructions
    - Example queries

Complete the database schema design ensuring it's scalable, performant, and maintainable.
