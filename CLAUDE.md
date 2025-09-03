# Papaya - AI Feedback System Refactoring Guide

## Project Overview

Papaya is a complete rewrite of the AI Feedback System using modern technologies to create a more maintainable, scalable, and beginner-friendly codebase. This project transforms a complex multi-service application into a streamlined Next.js full-stack application.

## Original Project Analysis

The original AI Feedback System (git@github.com:Summer-project-25-AI-Feedback-system/AI-Feedback-System.git) has several architectural challenges:

### Current Architecture Issues

- **Complexity**: Separate client, server, and API services create unnecessary complexity
- **Code Duplication**: Similar files (`Aievalutions.ts`, `Aievolution.ts`) suggest duplicate logic
- **Multiple Technologies**: React+Vite frontend, Express.js backend, Supabase database creates maintenance overhead
- **Deployment Complexity**: Multiple services require complex orchestration
- **Learning Curve**: Difficult for beginners due to scattered architecture

### Current Tech Stack

- **Frontend**: React 19.1.0, Vite, TypeScript, TailwindCSS
- **Backend**: Node.js, Express.js, TypeScript
- **Database**: Supabase
- **Authentication**: Passport.js, GitHub OAuth
- **AI Integration**: OpenAI API
- **Deployment**: Docker, Docker Compose

## New Tech Stack & Rationale

### Technology Choices

#### Next.js 15+ (Full-Stack Framework)

- **Why**: Eliminates client/server separation complexity
- **Benefits**:
  - Server Components for better performance
  - API routes eliminate separate backend
  - Built-in optimization and deployment
  - Simpler project structure
  - Better SEO and loading performance

#### PostgreSQL + Prisma (Database Layer)

- **Why**: More mature than Supabase for learning, better performance
- **Benefits**:
  - Type-safe database operations
  - Excellent developer experience
  - Migration management
  - Better for production deployments
  - Clear schema definition

#### TailwindCSS (Styling)

- **Why**: Already used, proven effective
- **Benefits**: Utility-first approach, consistent design system

#### Docker + GHCR (Deployment)

- **Why**: Industry standard for modern deployments
- **Benefits**:
  - Consistent environments
  - Easy scaling
  - Production-ready
  - GitHub integration

## Stage-by-Stage Refactoring Plan

### Stage 1: Project Foundation & Landing Page 🚀

**Duration**: 1-2 weeks | **Complexity**: Beginner

#### Goals

- Set up modern development environment
- Create responsive landing page
- Establish design system and project structure

#### Learning Objectives

- Next.js project structure and configuration
- TailwindCSS design system principles
- Modern React patterns with TypeScript
- Docker development workflow

#### Tasks Breakdown

1. **Initialize Next.js Project** (Day 1)

   ```bash
   npx create-next-app@latest papaya --typescript --tailwind --app
   ```

   - Configure TypeScript strict mode
   - Set up ESLint and Prettier
   - Configure absolute imports

2. **Design System Setup** (Day 1-2)
   - Create `design-system.md` documenting colors, typography, spacing
   - Set up TailwindCSS custom configuration
   - Create reusable component primitives (Button, Input, Card)
   - Implement dark/light mode support

3. **Landing Page Components** (Day 3-5)
   - Hero section with value proposition
   - Features showcase (AI feedback, GitHub integration, dashboard)
   - Pricing/plans section
   - Testimonials or demo section
   - Call-to-action sections

4. **Navigation & Layout** (Day 6-7)
   - Responsive navigation header
   - Footer with links and information
   - Mobile-first responsive design
   - Accessibility considerations (ARIA labels, keyboard navigation)

5. **Docker Development Setup** (Day 7)
   - Create `Dockerfile.dev` for development
   - Set up `docker-compose.dev.yml`
   - Configure hot reloading in containers
   - Document development workflow

#### Acceptance Criteria

- [ ] Landing page loads on `localhost:3000`
- [ ] Fully responsive on mobile, tablet, desktop
- [ ] Dark/light mode toggle works
- [ ] Docker development environment functional
- [ ] All components accessible and semantic HTML

#### Files Created

- `app/page.tsx` - Landing page
- `components/ui/` - Reusable UI components
- `components/landing/` - Landing page specific components
- `lib/utils.ts` - Utility functions
- `docker-compose.dev.yml` - Development environment

---

### Stage 2: Authentication & User Management 🔐

**Duration**: 1-2 weeks | **Complexity**: Intermediate

#### Goals

- Implement secure authentication system
- Create user management functionality
- Set up role-based access control

#### Learning Objectives

- NextAuth.js configuration and providers
- JWT tokens and session management
- Role-based authorization patterns
- Secure route protection in Next.js

#### Tasks Breakdown

1. **NextAuth.js Setup** (Day 1-2)
   - Install and configure NextAuth.js
   - Set up GitHub OAuth provider
   - Configure JWT strategy
   - Create authentication pages (`/auth/signin`, `/auth/signup`)

2. **User Profile System** (Day 3-4)
   - Profile creation and editing forms
   - Avatar upload functionality
   - User preferences and settings
   - Account deletion and data export

3. **Role-Based Access Control** (Day 5-6)
   - Define user roles (student, professor, admin)
   - Create role assignment system
   - Implement middleware for route protection
   - Role-based UI component rendering

4. **Dashboard Layouts** (Day 7)
   - Student dashboard layout
   - Professor dashboard layout
   - Shared component architecture
   - Navigation based on user role

#### Acceptance Criteria

- [ ] Users can sign in with GitHub OAuth
- [ ] Profile management fully functional
- [ ] Role-based access properly enforced
- [ ] Protected routes redirect unauthenticated users
- [ ] Session management works correctly

#### Files Created

- `app/api/auth/[...nextauth]/route.ts` - NextAuth configuration
- `app/auth/` - Authentication pages
- `app/dashboard/` - Dashboard layouts
- `middleware.ts` - Route protection
- `lib/auth.ts` - Authentication utilities

---

### Stage 3: Database Schema & Core Models 🗄️

**Duration**: 1 week | **Complexity**: Intermediate

#### Goals

- Design comprehensive database schema
- Set up Prisma with PostgreSQL
- Create type-safe database operations

#### Learning Objectives

- Database design principles
- Prisma schema definition and migrations
- Type-safe database queries
- Data validation with Zod

#### Tasks Breakdown

1. **Database Schema Design** (Day 1-2)
   - Entity relationship diagram
   - Prisma schema definition
   - Index optimization for performance
   - Constraint and validation rules

2. **Prisma Setup** (Day 2-3)
   - PostgreSQL container configuration
   - Prisma client generation
   - Migration creation and testing
   - Database connection pooling

3. **Core Models Implementation** (Day 4-5)
   - User model with authentication
   - Assignment and submission models
   - Feedback and evaluation models
   - Relationship definitions

4. **Data Validation Layer** (Day 6-7)
   - Zod schema definitions
   - Input validation utilities
   - Error handling patterns
   - Type-safe API contracts

#### Acceptance Criteria

- [ ] Database migrations run successfully
- [ ] All CRUD operations work via Prisma
- [ ] Data validation prevents invalid inputs
- [ ] Type safety maintained across operations
- [ ] Database seeding script functional

#### Files Created

- `prisma/schema.prisma` - Database schema
- `lib/prisma.ts` - Database connection
- `lib/validations.ts` - Zod schemas
- `lib/db/` - Database operation functions

---

### Stage 4: Assignment Management System 📝

**Duration**: 2-3 weeks | **Complexity**: Advanced

#### Goals

- Build comprehensive assignment management
- Integrate with GitHub Classroom
- Create submission and tracking system

#### Learning Objectives

- Complex form handling in React
- GitHub API integration
- File upload and processing
- State management patterns

#### Tasks Breakdown

1. **Assignment Creation** (Day 1-3)
   - Multi-step assignment creation wizard
   - Rich text editor for descriptions
   - Due date and settings configuration
   - Assignment template system

2. **GitHub Integration** (Day 4-6)
   - GitHub Classroom API integration
   - Repository creation and management
   - Webhook handling for submissions
   - Branch and PR management

3. **Student Interface** (Day 7-9)
   - Assignment discovery and filtering
   - Submission interface
   - Progress tracking
   - Collaboration features

4. **File Management** (Day 10-12)
   - Code file upload and preview
   - Version control integration
   - Diff visualization
   - File validation and processing

#### Acceptance Criteria

- [ ] Professors can create and manage assignments
- [ ] GitHub Classroom integration functional
- [ ] Students can submit assignments
- [ ] File upload and processing works
- [ ] Assignment status tracking accurate

#### Files Created

- `app/assignments/` - Assignment management pages
- `components/assignments/` - Assignment components
- `lib/github.ts` - GitHub API integration
- `lib/file-processing.ts` - File handling utilities

---

### Stage 5: AI Integration & Feedback System 🤖

**Duration**: 2-3 weeks | **Complexity**: Advanced

#### Goals

- Implement AI-powered code evaluation
- Create intelligent feedback generation
- Build feedback management system

#### Learning Objectives

- OpenAI API integration and prompt engineering
- Async processing and job queues
- Code analysis techniques
- Feedback presentation patterns

#### Tasks Breakdown

1. **OpenAI Integration** (Day 1-3)
   - API key management and security
   - Prompt engineering for code evaluation
   - Response parsing and validation
   - Rate limiting and error handling

2. **Code Analysis Engine** (Day 4-7)
   - Static code analysis integration
   - Code quality metrics
   - Best practices checking
   - Language-specific evaluation

3. **Feedback Generation** (Day 8-10)
   - Intelligent feedback formatting
   - Severity levels and categories
   - Actionable improvement suggestions
   - Progress tracking over time

4. **Feedback Management** (Day 11-14)
   - Feedback history and versioning
   - Export to various formats
   - Bulk operations for professors
   - Student response system

#### Acceptance Criteria

- [ ] AI feedback generation functional
- [ ] Code analysis provides meaningful insights
- [ ] Feedback properly categorized and formatted
- [ ] Export functionality works for all formats
- [ ] Performance acceptable for multiple submissions

#### Files Created

- `lib/ai/` - AI integration modules
- `lib/code-analysis/` - Code analysis utilities
- `app/feedback/` - Feedback management pages
- `components/feedback/` - Feedback display components

---

### Stage 6: Dashboard & Analytics 📊

**Duration**: 2 weeks | **Complexity**: Intermediate

#### Goals

- Create comprehensive dashboards
- Implement analytics and reporting
- Build notification system

#### Learning Objectives

- Data visualization with charts
- Real-time updates and WebSockets
- Performance monitoring
- Notification patterns

#### Tasks Breakdown

1. **Dashboard Architecture** (Day 1-2)
   - Layout system for different roles
   - Widget-based dashboard components
   - Customizable dashboard configuration
   - Performance optimization

2. **Analytics Implementation** (Day 3-6)
   - Assignment completion statistics
   - Student progress tracking
   - Code quality trends
   - Performance metrics visualization

3. **Real-time Features** (Day 7-9)
   - Live submission updates
   - Real-time notifications
   - Activity feeds
   - Collaborative features

4. **Reporting System** (Day 10-12)
   - Automated report generation
   - Custom report builder
   - Scheduled reports
   - Export capabilities

#### Acceptance Criteria

- [ ] Dashboards display accurate real-time data
- [ ] Charts and visualizations functional
- [ ] Notifications work across all channels
- [ ] Reports generate correctly
- [ ] Performance meets requirements

#### Files Created

- `components/dashboard/` - Dashboard components
- `lib/analytics.ts` - Analytics utilities
- `lib/notifications.ts` - Notification system
- `app/reports/` - Reporting interface

---

### Stage 7: Production Deployment & DevOps 🚢

**Duration**: 1-2 weeks | **Complexity**: Advanced

#### Goals

- Set up production-ready deployment
- Implement CI/CD pipeline
- Configure monitoring and logging

#### Learning Objectives

- Docker production optimization
- GitHub Container Registry
- Environment management
- Monitoring and observability

#### Tasks Breakdown

1. **Production Docker Setup** (Day 1-3)
   - Multi-stage Docker builds
   - Security hardening
   - Resource optimization
   - Health checks and readiness probes

2. **CI/CD Pipeline** (Day 4-6)
   - GitHub Actions workflow
   - Automated testing integration
   - GHCR image building and pushing
   - Deployment automation

3. **Environment Management** (Day 7-9)
   - Environment-specific configurations
   - Secret management
   - Database migration automation
   - Backup strategies

4. **Monitoring & Logging** (Day 10-12)
   - Application performance monitoring
   - Error tracking and alerting
   - Log aggregation
   - Security monitoring

#### Acceptance Criteria

- [ ] Production deployment successful
- [ ] CI/CD pipeline fully functional
- [ ] Monitoring and alerting operational
- [ ] Security measures implemented
- [ ] Documentation complete

#### Files Created

- `Dockerfile.prod` - Production container
- `.github/workflows/` - CI/CD workflows
- `docker-compose.prod.yml` - Production compose
- `docs/deployment.md` - Deployment guide

---

### Stage 8: Testing & Documentation 🧪

**Duration**: 1-2 weeks | **Complexity**: Intermediate

#### Goals

- Implement comprehensive testing strategy
- Create thorough documentation
- Optimize performance and security

#### Learning Objectives

- Testing strategies and frameworks
- Documentation best practices
- Performance optimization techniques
- Security audit procedures

#### Tasks Breakdown

1. **Testing Implementation** (Day 1-5)
   - Unit tests for core functionality
   - Integration tests for API routes
   - End-to-end tests for user flows
   - Performance testing

2. **Documentation Creation** (Day 6-9)
   - API documentation
   - User guides and tutorials
   - Developer documentation
   - Troubleshooting guides

3. **Optimization & Security** (Day 10-12)
   - Performance profiling and optimization
   - Security audit and fixes
   - Accessibility improvements
   - Code quality improvements

#### Acceptance Criteria

- [ ] Full test suite with >80% coverage
- [ ] All documentation complete and accurate
- [ ] Performance benchmarks met
- [ ] Security audit passed
- [ ] Accessibility standards met

#### Files Created

- `__tests__/` - Test files
- `docs/` - Documentation
- `performance/` - Performance testing
- `security/` - Security configurations

## Development Guidelines

### Code Organization Principles

1. **Feature-Based Structure**: Group related files by feature, not by type
2. **Separation of Concerns**: Clear boundaries between UI, business logic, and data
3. **Reusability**: Create composable, reusable components and utilities
4. **Type Safety**: Leverage TypeScript for better developer experience
5. **Performance**: Optimize for Core Web Vitals and user experience

### Naming Conventions

- **Files**: kebab-case for files (`user-dashboard.tsx`)
- **Components**: PascalCase (`UserDashboard`)
- **Functions**: camelCase (`getUserData`)
- **Constants**: UPPER_SNAKE_CASE (`API_BASE_URL`)
- **Types**: PascalCase with descriptive names (`UserProfile`)

### Git Workflow

- **Branches**: `feature/stage-{number}-{description}`
- **Commits**: Conventional commits format
- **PRs**: One PR per stage with comprehensive testing
- **Reviews**: Self-review checklist before requesting review

## Learning Resources

### Essential Reading

- [Next.js Documentation](https://nextjs.org/docs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [TailwindCSS Documentation](https://tailwindcss.com/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs)

### Recommended Tutorials

- Next.js full-stack development
- Database design with Prisma
- Docker containerization
- Modern React patterns

## Troubleshooting Guide

### Common Issues & Solutions

#### Database Connection Issues

```bash
# Reset database
npm run db:reset
npm run db:seed
```

#### Docker Build Failures

```bash
# Clear Docker cache
docker system prune -a
docker-compose down -v
```

#### Type Errors

- Run `npm run type-check` to identify issues
- Ensure Prisma client is generated after schema changes

## Project Structure

```
papaya/
├── app/                 # Next.js app directory
│   ├── (auth)/         # Authentication pages
│   ├── dashboard/      # Dashboard pages
│   ├── assignments/    # Assignment management
│   ├── feedback/       # Feedback system
│   └── api/           # API routes
├── components/         # Reusable components
│   ├── ui/            # Base UI components
│   ├── forms/         # Form components
│   └── dashboard/     # Dashboard components
├── lib/               # Utility functions
│   ├── auth.ts        # Authentication utilities
│   ├── db.ts          # Database utilities
│   ├── validations.ts # Zod schemas
│   └── utils.ts       # General utilities
├── prisma/            # Database schema and migrations
├── docs/              # Documentation
├── __tests__/         # Test files
└── docker/            # Docker configurations
```

## Success Metrics

### Technical Metrics

- **Performance**: Core Web Vitals in green
- **Testing**: >80% code coverage
- **Security**: No critical vulnerabilities
- **Accessibility**: WCAG 2.1 AA compliance

### User Experience Metrics

- **Load Time**: <2 seconds initial page load
- **Navigation**: <500ms page transitions
- **Feedback Generation**: <30 seconds for typical submission
- **Mobile Experience**: Fully responsive and functional

### Learning Objectives Achieved

- Understanding of modern full-stack development
- Database design and management skills
- Deployment and DevOps practices
- Testing and documentation best practices

---

## Getting Started

Ready to begin your refactoring journey? Start with Stage 1 and work through each stage systematically. Remember:

1. **Test Early, Test Often**: Each stage should be fully functional before moving to the next
2. **Document Everything**: Keep notes on what you learn and any deviations from the plan
3. **Ask Questions**: Don't hesitate to ask for clarification or help
4. **Celebrate Progress**: Each completed stage is a significant achievement!

Good luck with your Papaya project! 🚀
