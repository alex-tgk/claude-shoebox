# Find and Fix Performance Issues

You are tasked with identifying and fixing performance issues in code to improve speed, efficiency, and resource usage.

## Instructions

1. **Identify Scope**
   - Ask which file(s), component(s), or feature to optimize
   - Understand performance goals (speed, memory, bundle size)
   - Ask if user has noticed specific slow operations
   - Check if performance metrics/benchmarks exist

2. **Performance Analysis**

   **Frontend (React/TypeScript):**
   - Identify unnecessary re-renders
   - Check for heavy computations in render
   - Analyze bundle size (large dependencies)
   - Look for unoptimized images/assets
   - Check for memory leaks
   - Identify expensive DOM operations
   - Review network request patterns
   - Check for render-blocking resources

   **Backend (Node.js/Go):**
   - Identify slow database queries
   - Check for N+1 query problems
   - Look for missing indexes
   - Identify synchronous blocking operations
   - Check for memory leaks
   - Review algorithm complexity
   - Analyze API response times
   - Check for inefficient loops

   **General:**
   - Look for O(n²) or worse algorithms
   - Identify unnecessary data processing
   - Check for redundant operations
   - Look for excessive memory usage
   - Identify blocking operations

3. **Frontend Optimization Techniques**

   **React Component Optimization:**
   - Use `React.memo()` for expensive components
   - Implement `useMemo()` for expensive calculations
   - Use `useCallback()` to prevent function recreation
   - Split large components into smaller ones
   - Use lazy loading with `React.lazy()` and Suspense
   - Avoid inline function definitions in JSX
   - Use key prop correctly in lists
   - Avoid anonymous objects in props

   **State Management:**
   - Minimize state updates
   - Move state closer to where it's used
   - Use context selectively (avoid over-context-ing)
   - Consider state management libraries for complex state
   - Batch state updates when possible

   **Bundle Optimization:**
   - Use dynamic imports for code splitting
   - Analyze bundle size with webpack-bundle-analyzer
   - Remove unused dependencies
   - Use tree-shaking effectively
   - Optimize imports (import only what you need)
   - Use lighter alternatives to heavy libraries

   **Asset Optimization:**
   - Compress images (WebP format)
   - Use lazy loading for images
   - Implement virtual scrolling for long lists
   - Optimize fonts (subset, preload)
   - Minify CSS/JS

   **Network Optimization:**
   - Implement caching strategies
   - Use CDN for static assets
   - Reduce API calls (combine requests)
   - Implement request debouncing/throttling
   - Use pagination for large datasets
   - Implement optimistic UI updates

4. **Backend Optimization Techniques**

   **Database Optimization:**
   - Add missing indexes
   - Optimize queries (use EXPLAIN)
   - Fix N+1 query problems (use joins, includes)
   - Use database connection pooling
   - Implement query caching
   - Use select only needed columns
   - Batch database operations

   **Algorithm Optimization:**
   - Replace inefficient algorithms
   - Use appropriate data structures
   - Reduce nested loops
   - Use memoization for repeated calculations
   - Implement caching for expensive operations

   **Concurrency:**
   - Use async/await properly
   - Implement parallel processing where applicable
   - Use worker threads for CPU-intensive tasks
   - Use goroutines effectively (Go)
   - Avoid blocking the event loop (Node.js)

   **Memory Optimization:**
   - Fix memory leaks
   - Use streams for large files
   - Clear unused references
   - Implement garbage collection optimization
   - Reduce object creation in hot paths

   **Caching:**
   - Implement Redis/in-memory caching
   - Use HTTP caching headers
   - Cache computed results
   - Use CDN for static content
   - Implement cache invalidation strategy

5. **Measurement and Benchmarking**

   **Before Optimization:**
   - Measure current performance
   - Create benchmarks
   - Document baseline metrics
   - Identify bottlenecks with profiling

   **Frontend Metrics:**
   - Use React DevTools Profiler
   - Measure Lighthouse scores
   - Check Core Web Vitals (LCP, FID, CLS)
   - Measure bundle size
   - Use Chrome DevTools Performance tab

   **Backend Metrics:**
   - Measure API response times
   - Check database query times
   - Monitor memory usage
   - Track CPU usage
   - Use profiling tools (node --prof, pprof)

   **After Optimization:**
   - Re-measure all metrics
   - Compare before/after results
   - Document improvements
   - Ensure no regressions

6. **Implementation Process**
   - Start with the biggest bottlenecks
   - Make one optimization at a time
   - Measure impact after each change
   - Run tests after each optimization
   - Profile again to find next bottleneck
   - Document optimizations made

7. **Testing**
   - Ensure all tests still pass
   - Add performance tests if applicable
   - Test with realistic data volumes
   - Test on different devices/browsers
   - Test under load (stress testing)
   - Check for edge cases

8. **Trade-offs and Considerations**
   - Balance performance vs. code readability
   - Consider maintenance burden
   - Don't over-optimize
   - Focus on user-facing performance
   - Consider premature optimization risks
   - Document complex optimizations

9. **Final Report**

   Provide comprehensive report including:
   - Performance issues identified
   - Optimizations implemented
   - Before/after metrics comparison
   - Performance improvements achieved
   - Code changes made
   - Any trade-offs accepted
   - Recommendations for monitoring
   - Future optimization opportunities

Complete the optimization process and provide detailed metrics showing the improvements.
