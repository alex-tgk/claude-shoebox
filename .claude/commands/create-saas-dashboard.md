# Create SaaS Dashboard

Generate a complete, production-ready SaaS admin dashboard with professional UI, real-time updates, user management, analytics, and billing integration.

## Instructions

You are tasked with creating a COMPLETE, production-ready SaaS dashboard. This is a one-shot command that must produce a fully functional, polished admin interface ready for immediate deployment.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **SaaS Product**: What type of SaaS application is this for?
2. **User Roles**: What user roles exist? (Admin, Manager, User, etc.)
3. **Key Metrics**: What are the 5-10 most important metrics to display?
4. **Tech Stack**: React, Vue, or Angular? TypeScript preference?
5. **Backend**: Existing API or need to create mock endpoints?
6. **Authentication**: Existing auth system or need to implement?
7. **Billing**: Stripe, Paddle, or other payment provider?
8. **Real-time Updates**: WebSocket, polling, or Server-Sent Events?

### Step 2: Complete Dashboard Structure

Create the following COMPLETE structure:

```
saas-dashboard/
├── src/
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Header.tsx
│   │   │   ├── Footer.tsx
│   │   │   └── DashboardLayout.tsx
│   │   ├── charts/
│   │   │   ├── LineChart.tsx
│   │   │   ├── BarChart.tsx
│   │   │   ├── PieChart.tsx
│   │   │   ├── AreaChart.tsx
│   │   │   └── MetricCard.tsx
│   │   ├── tables/
│   │   │   ├── DataTable.tsx
│   │   │   ├── TablePagination.tsx
│   │   │   ├── TableFilters.tsx
│   │   │   └── TableActions.tsx
│   │   ├── forms/
│   │   │   ├── Input.tsx
│   │   │   ├── Select.tsx
│   │   │   ├── Textarea.tsx
│   │   │   ├── DatePicker.tsx
│   │   │   └── FileUpload.tsx
│   │   ├── modals/
│   │   │   ├── Modal.tsx
│   │   │   ├── ConfirmDialog.tsx
│   │   │   └── UserEditModal.tsx
│   │   └── common/
│   │       ├── Button.tsx
│   │       ├── Badge.tsx
│   │       ├── Avatar.tsx
│   │       ├── Tooltip.tsx
│   │       ├── Dropdown.tsx
│   │       ├── Tabs.tsx
│   │       └── LoadingSpinner.tsx
│   ├── pages/
│   │   ├── Dashboard/
│   │   │   ├── Overview.tsx
│   │   │   └── components/
│   │   ├── Analytics/
│   │   │   ├── index.tsx
│   │   │   ├── Revenue.tsx
│   │   │   ├── Users.tsx
│   │   │   └── Traffic.tsx
│   │   ├── Users/
│   │   │   ├── UserList.tsx
│   │   │   ├── UserDetail.tsx
│   │   │   └── UserActivity.tsx
│   │   ├── Settings/
│   │   │   ├── Profile.tsx
│   │   │   ├── Team.tsx
│   │   │   ├── Billing.tsx
│   │   │   ├── Integrations.tsx
│   │   │   └── Security.tsx
│   │   ├── Billing/
│   │   │   ├── Subscription.tsx
│   │   │   ├── Invoices.tsx
│   │   │   └── PaymentMethods.tsx
│   │   └── Auth/
│   │       ├── Login.tsx
│   │       ├── Register.tsx
│   │       └── ForgotPassword.tsx
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── useWebSocket.ts
│   │   ├── useApi.ts
│   │   ├── useTheme.ts
│   │   └── useAnalytics.ts
│   ├── services/
│   │   ├── api.ts
│   │   ├── auth.ts
│   │   ├── websocket.ts
│   │   ├── analytics.ts
│   │   └── billing.ts
│   ├── store/
│   │   ├── auth.ts
│   │   ├── users.ts
│   │   ├── dashboard.ts
│   │   └── settings.ts
│   ├── utils/
│   │   ├── formatters.ts
│   │   ├── validators.ts
│   │   ├── constants.ts
│   │   └── helpers.ts
│   ├── styles/
│   │   ├── globals.css
│   │   ├── variables.css
│   │   └── themes/
│   │       ├── light.css
│   │       └── dark.css
│   └── types/
│       ├── user.ts
│       ├── dashboard.ts
│       └── api.ts
├── public/
│   ├── images/
│   └── icons/
├── tests/
│   ├── components/
│   └── pages/
├── .env.example
├── tailwind.config.js
├── tsconfig.json
├── package.json
└── README.md
```

### Step 3: Implement Complete Dashboard Layout

#### Sidebar Navigation

```typescript
// components/layout/Sidebar.tsx
import { useState } from 'react';
import { Link, useLocation } from 'react-router-dom';
import {
  HomeIcon,
  ChartBarIcon,
  UsersIcon,
  CogIcon,
  CreditCardIcon,
  BellIcon,
  DocumentIcon,
  ShieldCheckIcon
} from '@heroicons/react/24/outline';

const menuItems = [
  { name: 'Overview', href: '/dashboard', icon: HomeIcon },
  { name: 'Analytics', href: '/analytics', icon: ChartBarIcon },
  { name: 'Users', href: '/users', icon: UsersIcon, badge: '124' },
  { name: 'Billing', href: '/billing', icon: CreditCardIcon },
  { name: 'Settings', href: '/settings', icon: CogIcon },
];

const Sidebar = () => {
  const [collapsed, setCollapsed] = useState(false);
  const location = useLocation();

  const isActive = (href: string) => location.pathname === href;

  return (
    <aside className={`bg-gray-900 text-white h-screen fixed left-0 top-0 transition-all ${
      collapsed ? 'w-16' : 'w-64'
    }`}>
      {/* Logo */}
      <div className="h-16 flex items-center justify-between px-4 border-b border-gray-800">
        {!collapsed && (
          <h1 className="text-xl font-bold">YourSaaS</h1>
        )}
        <button
          onClick={() => setCollapsed(!collapsed)}
          className="p-2 hover:bg-gray-800 rounded"
        >
          {/* Toggle icon */}
        </button>
      </div>

      {/* Navigation */}
      <nav className="mt-6">
        {menuItems.map((item) => (
          <Link
            key={item.name}
            to={item.href}
            className={`flex items-center px-4 py-3 hover:bg-gray-800 transition-colors ${
              isActive(item.href) ? 'bg-gray-800 border-l-4 border-blue-500' : ''
            }`}
          >
            <item.icon className="h-6 w-6" />
            {!collapsed && (
              <>
                <span className="ml-3">{item.name}</span>
                {item.badge && (
                  <span className="ml-auto bg-blue-500 text-xs px-2 py-1 rounded-full">
                    {item.badge}
                  </span>
                )}
              </>
            )}
          </Link>
        ))}
      </nav>

      {/* User Profile */}
      <div className="absolute bottom-0 left-0 right-0 p-4 border-t border-gray-800">
        <div className="flex items-center">
          <img
            src="/avatar.jpg"
            alt="Profile"
            className="h-10 w-10 rounded-full"
          />
          {!collapsed && (
            <div className="ml-3">
              <p className="text-sm font-medium">John Doe</p>
              <p className="text-xs text-gray-400">john@example.com</p>
            </div>
          )}
        </div>
      </div>
    </aside>
  );
};

export default Sidebar;
```

#### Header Component

```typescript
// components/layout/Header.tsx
import { useState } from 'react';
import { BellIcon, MagnifyingGlassIcon, MoonIcon, SunIcon } from '@heroicons/react/24/outline';

const Header = () => {
  const [darkMode, setDarkMode] = useState(false);
  const [notifications, setNotifications] = useState(3);

  return (
    <header className="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 h-16 fixed top-0 right-0 left-64 z-10">
      <div className="h-full px-6 flex items-center justify-between">
        {/* Search */}
        <div className="flex-1 max-w-md">
          <div className="relative">
            <MagnifyingGlassIcon className="absolute left-3 top-1/2 transform -translate-y-1/2 h-5 w-5 text-gray-400" />
            <input
              type="text"
              placeholder="Search..."
              className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
          </div>
        </div>

        {/* Actions */}
        <div className="flex items-center space-x-4">
          {/* Theme Toggle */}
          <button
            onClick={() => setDarkMode(!darkMode)}
            className="p-2 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-lg"
          >
            {darkMode ? <SunIcon className="h-5 w-5" /> : <MoonIcon className="h-5 w-5" />}
          </button>

          {/* Notifications */}
          <button className="relative p-2 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-lg">
            <BellIcon className="h-5 w-5" />
            {notifications > 0 && (
              <span className="absolute top-0 right-0 h-4 w-4 bg-red-500 text-white text-xs rounded-full flex items-center justify-center">
                {notifications}
              </span>
            )}
          </button>

          {/* Profile Dropdown */}
          <div className="relative">
            {/* Profile menu */}
          </div>
        </div>
      </div>
    </header>
  );
};

export default Header;
```

### Step 4: Dashboard Overview Page

```typescript
// pages/Dashboard/Overview.tsx
import { useEffect, useState } from 'react';
import MetricCard from '../../components/charts/MetricCard';
import LineChart from '../../components/charts/LineChart';
import BarChart from '../../components/charts/BarChart';
import { useWebSocket } from '../../hooks/useWebSocket';

const Overview = () => {
  const [metrics, setMetrics] = useState({
    revenue: { value: 45231.89, change: 12.5, trend: 'up' },
    users: { value: 2350, change: 8.2, trend: 'up' },
    orders: { value: 1429, change: -3.1, trend: 'down' },
    conversion: { value: 3.24, change: 5.7, trend: 'up' }
  });

  // Real-time updates via WebSocket
  useWebSocket('/ws/dashboard', (data) => {
    setMetrics(prev => ({
      ...prev,
      ...data
    }));
  });

  return (
    <div className="p-6">
      {/* Page Header */}
      <div className="mb-6">
        <h1 className="text-2xl font-bold text-gray-900 dark:text-white">
          Dashboard Overview
        </h1>
        <p className="text-gray-600 dark:text-gray-400">
          Welcome back! Here's what's happening with your business today.
        </p>
      </div>

      {/* Metrics Grid */}
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
        <MetricCard
          title="Total Revenue"
          value={`$${metrics.revenue.value.toLocaleString()}`}
          change={metrics.revenue.change}
          trend={metrics.revenue.trend}
          icon="currency"
        />
        <MetricCard
          title="Active Users"
          value={metrics.users.value.toLocaleString()}
          change={metrics.users.change}
          trend={metrics.users.trend}
          icon="users"
        />
        <MetricCard
          title="Total Orders"
          value={metrics.orders.value.toLocaleString()}
          change={metrics.orders.change}
          trend={metrics.orders.trend}
          icon="shopping"
        />
        <MetricCard
          title="Conversion Rate"
          value={`${metrics.conversion.value}%`}
          change={metrics.conversion.change}
          trend={metrics.conversion.trend}
          icon="chart"
        />
      </div>

      {/* Charts Grid */}
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-6">
        {/* Revenue Chart */}
        <div className="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
          <div className="flex items-center justify-between mb-4">
            <h2 className="text-lg font-semibold">Revenue Overview</h2>
            <select className="text-sm border rounded px-3 py-1">
              <option>Last 7 days</option>
              <option>Last 30 days</option>
              <option>Last 90 days</option>
            </select>
          </div>
          <LineChart
            data={revenueData}
            xKey="date"
            yKey="revenue"
            color="#3B82F6"
          />
        </div>

        {/* User Growth Chart */}
        <div className="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
          <div className="flex items-center justify-between mb-4">
            <h2 className="text-lg font-semibold">User Growth</h2>
            <select className="text-sm border rounded px-3 py-1">
              <option>Monthly</option>
              <option>Weekly</option>
              <option>Daily</option>
            </select>
          </div>
          <BarChart
            data={userGrowthData}
            xKey="month"
            yKey="users"
            color="#10B981"
          />
        </div>
      </div>

      {/* Recent Activity & Top Products */}
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
        {/* Recent Activity */}
        <div className="bg-white dark:bg-gray-800 rounded-lg shadow">
          <div className="p-6 border-b border-gray-200 dark:border-gray-700">
            <h2 className="text-lg font-semibold">Recent Activity</h2>
          </div>
          <div className="divide-y divide-gray-200 dark:divide-gray-700">
            {recentActivity.map((activity) => (
              <div key={activity.id} className="p-4 flex items-start">
                <div className={`p-2 rounded-full bg-${activity.color}-100`}>
                  {activity.icon}
                </div>
                <div className="ml-3 flex-1">
                  <p className="text-sm font-medium">{activity.title}</p>
                  <p className="text-xs text-gray-500">{activity.description}</p>
                  <p className="text-xs text-gray-400 mt-1">{activity.time}</p>
                </div>
              </div>
            ))}
          </div>
        </div>

        {/* Top Products */}
        <div className="bg-white dark:bg-gray-800 rounded-lg shadow">
          <div className="p-6 border-b border-gray-200 dark:border-gray-700">
            <h2 className="text-lg font-semibold">Top Products</h2>
          </div>
          <div className="p-6">
            {topProducts.map((product, index) => (
              <div key={product.id} className="flex items-center justify-between mb-4">
                <div className="flex items-center">
                  <span className="text-lg font-bold text-gray-400 w-8">
                    #{index + 1}
                  </span>
                  <img
                    src={product.image}
                    alt={product.name}
                    className="h-10 w-10 rounded object-cover ml-2"
                  />
                  <div className="ml-3">
                    <p className="text-sm font-medium">{product.name}</p>
                    <p className="text-xs text-gray-500">{product.sales} sales</p>
                  </div>
                </div>
                <p className="text-sm font-semibold">${product.revenue}</p>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
};

export default Overview;
```

### Step 5: Analytics Page

```typescript
// pages/Analytics/index.tsx
import { useState } from 'react';
import { DateRangePicker } from '../../components/forms/DatePicker';
import LineChart from '../../components/charts/LineChart';
import AreaChart from '../../components/charts/AreaChart';
import PieChart from '../../components/charts/PieChart';

const Analytics = () => {
  const [dateRange, setDateRange] = useState({
    start: new Date(Date.now() - 30 * 24 * 60 * 60 * 1000),
    end: new Date()
  });

  return (
    <div className="p-6">
      {/* Header with Filters */}
      <div className="mb-6 flex items-center justify-between">
        <div>
          <h1 className="text-2xl font-bold">Analytics</h1>
          <p className="text-gray-600">Deep dive into your business metrics</p>
        </div>
        <div className="flex items-center space-x-4">
          <DateRangePicker value={dateRange} onChange={setDateRange} />
          <button className="btn btn-primary">Export Report</button>
        </div>
      </div>

      {/* KPIs */}
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
        {kpis.map(kpi => (
          <div key={kpi.id} className="bg-white rounded-lg shadow p-6">
            <div className="flex items-center justify-between mb-2">
              <span className="text-sm text-gray-600">{kpi.label}</span>
              <span className={`text-sm font-medium ${
                kpi.trend === 'up' ? 'text-green-600' : 'text-red-600'
              }`}>
                {kpi.trend === 'up' ? '↑' : '↓'} {kpi.change}%
              </span>
            </div>
            <div className="text-3xl font-bold">{kpi.value}</div>
            <div className="mt-2 text-xs text-gray-500">
              vs. previous period: {kpi.previous}
            </div>
          </div>
        ))}
      </div>

      {/* Charts */}
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-6">
        {/* Revenue Trend */}
        <div className="bg-white rounded-lg shadow p-6 col-span-2">
          <h2 className="text-lg font-semibold mb-4">Revenue Trend</h2>
          <AreaChart
            data={revenueTrendData}
            xKey="date"
            yKeys={['revenue', 'profit', 'expenses']}
            colors={['#3B82F6', '#10B981', '#EF4444']}
            height={300}
          />
        </div>

        {/* Traffic Sources */}
        <div className="bg-white rounded-lg shadow p-6">
          <h2 className="text-lg font-semibold mb-4">Traffic Sources</h2>
          <PieChart
            data={trafficSourcesData}
            labelKey="source"
            valueKey="visitors"
          />
        </div>

        {/* Conversion Funnel */}
        <div className="bg-white rounded-lg shadow p-6">
          <h2 className="text-lg font-semibold mb-4">Conversion Funnel</h2>
          <div className="space-y-4">
            {funnelData.map((stage, index) => (
              <div key={stage.name}>
                <div className="flex items-center justify-between mb-2">
                  <span className="text-sm font-medium">{stage.name}</span>
                  <span className="text-sm text-gray-600">
                    {stage.users} ({stage.percentage}%)
                  </span>
                </div>
                <div className="w-full bg-gray-200 rounded-full h-3">
                  <div
                    className="bg-blue-600 h-3 rounded-full transition-all"
                    style={{ width: `${stage.percentage}%` }}
                  />
                </div>
                {index < funnelData.length - 1 && (
                  <div className="text-xs text-red-600 mt-1">
                    ↓ {stage.dropoff}% drop-off
                  </div>
                )}
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Detailed Tables */}
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
        {/* Top Pages */}
        <div className="bg-white rounded-lg shadow">
          <div className="p-6 border-b">
            <h2 className="text-lg font-semibold">Top Pages</h2>
          </div>
          <table className="w-full">
            <thead className="bg-gray-50">
              <tr>
                <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                  Page
                </th>
                <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                  Views
                </th>
                <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                  Avg. Time
                </th>
              </tr>
            </thead>
            <tbody className="divide-y divide-gray-200">
              {topPages.map(page => (
                <tr key={page.path}>
                  <td className="px-6 py-4 text-sm">{page.path}</td>
                  <td className="px-6 py-4 text-sm">{page.views}</td>
                  <td className="px-6 py-4 text-sm">{page.avgTime}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>

        {/* Geographic Distribution */}
        <div className="bg-white rounded-lg shadow">
          <div className="p-6 border-b">
            <h2 className="text-lg font-semibold">Top Countries</h2>
          </div>
          <table className="w-full">
            <thead className="bg-gray-50">
              <tr>
                <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                  Country
                </th>
                <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                  Users
                </th>
                <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                  Revenue
                </th>
              </tr>
            </thead>
            <tbody className="divide-y divide-gray-200">
              {topCountries.map(country => (
                <tr key={country.code}>
                  <td className="px-6 py-4 text-sm flex items-center">
                    <img src={`/flags/${country.code}.svg`} className="h-4 w-6 mr-2" />
                    {country.name}
                  </td>
                  <td className="px-6 py-4 text-sm">{country.users}</td>
                  <td className="px-6 py-4 text-sm">${country.revenue}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>
    </div>
  );
};

export default Analytics;
```

### Step 6: User Management

```typescript
// pages/Users/UserList.tsx
import { useState } from 'react';
import DataTable from '../../components/tables/DataTable';
import UserEditModal from '../../components/modals/UserEditModal';

const UserList = () => {
  const [users, setUsers] = useState([]);
  const [selectedUser, setSelectedUser] = useState(null);
  const [showModal, setShowModal] = useState(false);
  const [filters, setFilters] = useState({
    search: '',
    role: 'all',
    status: 'all'
  });

  const columns = [
    {
      key: 'name',
      label: 'User',
      render: (user) => (
        <div className="flex items-center">
          <img
            src={user.avatar}
            alt={user.name}
            className="h-10 w-10 rounded-full"
          />
          <div className="ml-3">
            <p className="text-sm font-medium">{user.name}</p>
            <p className="text-xs text-gray-500">{user.email}</p>
          </div>
        </div>
      )
    },
    {
      key: 'role',
      label: 'Role',
      render: (user) => (
        <span className={`px-2 py-1 text-xs rounded-full ${
          user.role === 'admin' ? 'bg-purple-100 text-purple-800' :
          user.role === 'manager' ? 'bg-blue-100 text-blue-800' :
          'bg-gray-100 text-gray-800'
        }`}>
          {user.role}
        </span>
      )
    },
    {
      key: 'status',
      label: 'Status',
      render: (user) => (
        <span className={`px-2 py-1 text-xs rounded-full ${
          user.status === 'active' ? 'bg-green-100 text-green-800' :
          'bg-red-100 text-red-800'
        }`}>
          {user.status}
        </span>
      )
    },
    {
      key: 'lastActive',
      label: 'Last Active',
      render: (user) => (
        <span className="text-sm text-gray-600">
          {formatRelativeTime(user.lastActive)}
        </span>
      )
    },
    {
      key: 'actions',
      label: 'Actions',
      render: (user) => (
        <div className="flex space-x-2">
          <button
            onClick={() => handleEdit(user)}
            className="text-blue-600 hover:text-blue-800"
          >
            Edit
          </button>
          <button
            onClick={() => handleDelete(user)}
            className="text-red-600 hover:text-red-800"
          >
            Delete
          </button>
        </div>
      )
    }
  ];

  const handleEdit = (user) => {
    setSelectedUser(user);
    setShowModal(true);
  };

  const handleDelete = async (user) => {
    if (confirm(`Delete user ${user.name}?`)) {
      await api.users.delete(user.id);
      fetchUsers();
    }
  };

  return (
    <div className="p-6">
      {/* Header */}
      <div className="mb-6 flex items-center justify-between">
        <div>
          <h1 className="text-2xl font-bold">Users</h1>
          <p className="text-gray-600">Manage your team and users</p>
        </div>
        <button
          onClick={() => setShowModal(true)}
          className="btn btn-primary"
        >
          Add User
        </button>
      </div>

      {/* Filters */}
      <div className="mb-6 grid grid-cols-1 md:grid-cols-4 gap-4">
        <input
          type="text"
          placeholder="Search users..."
          value={filters.search}
          onChange={(e) => setFilters({ ...filters, search: e.target.value })}
          className="px-4 py-2 border rounded-lg"
        />
        <select
          value={filters.role}
          onChange={(e) => setFilters({ ...filters, role: e.target.value })}
          className="px-4 py-2 border rounded-lg"
        >
          <option value="all">All Roles</option>
          <option value="admin">Admin</option>
          <option value="manager">Manager</option>
          <option value="user">User</option>
        </select>
        <select
          value={filters.status}
          onChange={(e) => setFilters({ ...filters, status: e.target.value })}
          className="px-4 py-2 border rounded-lg"
        >
          <option value="all">All Status</option>
          <option value="active">Active</option>
          <option value="inactive">Inactive</option>
        </select>
        <button
          onClick={() => exportUsers()}
          className="btn btn-secondary"
        >
          Export CSV
        </button>
      </div>

      {/* Table */}
      <DataTable
        data={users}
        columns={columns}
        pagination
        pageSize={10}
      />

      {/* Edit Modal */}
      {showModal && (
        <UserEditModal
          user={selectedUser}
          onClose={() => setShowModal(false)}
          onSave={(user) => {
            saveUser(user);
            setShowModal(false);
          }}
        />
      )}
    </div>
  );
};

export default UserList;
```

### Step 7: Billing Integration

```typescript
// pages/Billing/Subscription.tsx
import { useState, useEffect } from 'react';
import { loadStripe } from '@stripe/stripe-js';
import { Elements, CardElement, useStripe, useElements } from '@stripe/react-stripe-js';

const stripePromise = loadStripe(process.env.REACT_APP_STRIPE_PUBLIC_KEY);

const Subscription = () => {
  const [currentPlan, setCurrentPlan] = useState(null);
  const [plans, setPlans] = useState([
    {
      id: 'starter',
      name: 'Starter',
      price: 29,
      interval: 'month',
      features: [
        'Up to 10 users',
        'Basic analytics',
        'Email support',
        '10GB storage'
      ]
    },
    {
      id: 'professional',
      name: 'Professional',
      price: 79,
      interval: 'month',
      popular: true,
      features: [
        'Up to 50 users',
        'Advanced analytics',
        'Priority support',
        '100GB storage',
        'Custom integrations',
        'API access'
      ]
    },
    {
      id: 'enterprise',
      name: 'Enterprise',
      price: 199,
      interval: 'month',
      features: [
        'Unlimited users',
        'Enterprise analytics',
        '24/7 support',
        'Unlimited storage',
        'Custom integrations',
        'Dedicated account manager',
        'SLA guarantee'
      ]
    }
  ]);

  useEffect(() => {
    fetchCurrentSubscription();
  }, []);

  const fetchCurrentSubscription = async () => {
    const subscription = await api.billing.getCurrentSubscription();
    setCurrentPlan(subscription);
  };

  const handleUpgrade = async (planId) => {
    try {
      const { clientSecret } = await api.billing.createSubscription(planId);
      // Handle Stripe checkout
      const stripe = await stripePromise;
      await stripe.confirmCardPayment(clientSecret);
      fetchCurrentSubscription();
    } catch (error) {
      console.error('Subscription error:', error);
    }
  };

  return (
    <div className="p-6">
      {/* Current Plan */}
      {currentPlan && (
        <div className="mb-8 bg-blue-50 border border-blue-200 rounded-lg p-6">
          <div className="flex items-center justify-between">
            <div>
              <h2 className="text-lg font-semibold">Current Plan: {currentPlan.name}</h2>
              <p className="text-gray-600">
                ${currentPlan.price}/month • Next billing date: {currentPlan.nextBillingDate}
              </p>
            </div>
            <button className="btn btn-secondary">Manage Plan</button>
          </div>
        </div>
      )}

      {/* Plans */}
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {plans.map(plan => (
          <div
            key={plan.id}
            className={`bg-white rounded-lg shadow-lg overflow-hidden ${
              plan.popular ? 'ring-2 ring-blue-500' : ''
            }`}
          >
            {plan.popular && (
              <div className="bg-blue-500 text-white text-center py-2 text-sm font-medium">
                Most Popular
              </div>
            )}
            <div className="p-6">
              <h3 className="text-xl font-bold mb-2">{plan.name}</h3>
              <div className="mb-4">
                <span className="text-4xl font-bold">${plan.price}</span>
                <span className="text-gray-600">/{plan.interval}</span>
              </div>
              <ul className="space-y-3 mb-6">
                {plan.features.map((feature, index) => (
                  <li key={index} className="flex items-start">
                    <svg className="h-5 w-5 text-green-500 mr-2 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
                      <path fillRule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clipRule="evenodd" />
                    </svg>
                    <span className="text-sm">{feature}</span>
                  </li>
                ))}
              </ul>
              <button
                onClick={() => handleUpgrade(plan.id)}
                className={`w-full py-3 rounded-lg font-medium ${
                  currentPlan?.id === plan.id
                    ? 'bg-gray-200 text-gray-700 cursor-not-allowed'
                    : 'bg-blue-600 text-white hover:bg-blue-700'
                }`}
                disabled={currentPlan?.id === plan.id}
              >
                {currentPlan?.id === plan.id ? 'Current Plan' : 'Upgrade'}
              </button>
            </div>
          </div>
        ))}
      </div>

      {/* Billing History */}
      <div className="mt-12 bg-white rounded-lg shadow">
        <div className="p-6 border-b">
          <h2 className="text-lg font-semibold">Billing History</h2>
        </div>
        <table className="w-full">
          <thead className="bg-gray-50">
            <tr>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                Date
              </th>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                Description
              </th>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                Amount
              </th>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                Status
              </th>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">
                Invoice
              </th>
            </tr>
          </thead>
          <tbody className="divide-y divide-gray-200">
            {invoices.map(invoice => (
              <tr key={invoice.id}>
                <td className="px-6 py-4 text-sm">{invoice.date}</td>
                <td className="px-6 py-4 text-sm">{invoice.description}</td>
                <td className="px-6 py-4 text-sm">${invoice.amount}</td>
                <td className="px-6 py-4 text-sm">
                  <span className={`px-2 py-1 text-xs rounded-full ${
                    invoice.status === 'paid' ? 'bg-green-100 text-green-800' : 'bg-yellow-100 text-yellow-800'
                  }`}>
                    {invoice.status}
                  </span>
                </td>
                <td className="px-6 py-4 text-sm">
                  <a href={invoice.pdf} className="text-blue-600 hover:underline">
                    Download
                  </a>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
};

export default Subscription;
```

### Step 8: Real-time Updates

```typescript
// hooks/useWebSocket.ts
import { useEffect, useRef } from 'react';

export const useWebSocket = (endpoint: string, onMessage: (data: any) => void) => {
  const ws = useRef<WebSocket | null>(null);

  useEffect(() => {
    // Connect to WebSocket
    const wsUrl = `${process.env.REACT_APP_WS_URL}${endpoint}`;
    ws.current = new WebSocket(wsUrl);

    ws.current.onopen = () => {
      console.log('WebSocket connected');
    };

    ws.current.onmessage = (event) => {
      const data = JSON.parse(event.data);
      onMessage(data);
    };

    ws.current.onerror = (error) => {
      console.error('WebSocket error:', error);
    };

    ws.current.onclose = () => {
      console.log('WebSocket disconnected');
      // Reconnect after 5 seconds
      setTimeout(() => {
        // Reconnect logic
      }, 5000);
    };

    // Cleanup
    return () => {
      if (ws.current) {
        ws.current.close();
      }
    };
  }, [endpoint]);

  const send = (data: any) => {
    if (ws.current && ws.current.readyState === WebSocket.OPEN) {
      ws.current.send(JSON.stringify(data));
    }
  };

  return { send };
};
```

### Step 9: Dark Mode Support

```css
/* styles/themes/dark.css */
:root.dark {
  --bg-primary: #1a202c;
  --bg-secondary: #2d3748;
  --text-primary: #f7fafc;
  --text-secondary: #e2e8f0;
  --border-color: #4a5568;
  --accent-color: #3b82f6;
}

/* styles/globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components {
  .btn {
    @apply px-4 py-2 rounded-lg font-medium transition-colors;
  }

  .btn-primary {
    @apply bg-blue-600 text-white hover:bg-blue-700;
  }

  .btn-secondary {
    @apply bg-gray-200 text-gray-800 hover:bg-gray-300;
  }

  .card {
    @apply bg-white dark:bg-gray-800 rounded-lg shadow;
  }
}
```

### Step 10: Complete Documentation

```markdown
# SaaS Dashboard Documentation

## Overview
Production-ready SaaS dashboard with real-time analytics, user management, billing, and dark mode support.

## Features
✅ Responsive layout with sidebar navigation
✅ Real-time data updates via WebSocket
✅ User management with CRUD operations
✅ Role-based access control
✅ Analytics and reporting
✅ Stripe billing integration
✅ Dark mode support
✅ Chart visualizations
✅ Export functionality

## Setup

### Installation
\`\`\`bash
npm install
\`\`\`

### Environment Variables
\`\`\`
REACT_APP_API_URL=https://api.yourdomain.com
REACT_APP_WS_URL=wss://api.yourdomain.com
REACT_APP_STRIPE_PUBLIC_KEY=pk_test_xxx
\`\`\`

### Development
\`\`\`bash
npm start
\`\`\`

### Build
\`\`\`bash
npm run build
\`\`\`

## License
MIT
```

### Success Criteria

The command is successful when you deliver:
✅ Complete SaaS dashboard with all pages
✅ Responsive sidebar navigation
✅ Dashboard overview with metrics
✅ Analytics page with charts
✅ User management (list, edit, delete)
✅ Billing integration with Stripe
✅ Real-time updates via WebSocket
✅ Dark mode support
✅ Professional UI components
✅ Complete documentation

This should be a COMPLETE, PRODUCTION-READY SaaS dashboard ready for immediate deployment.
