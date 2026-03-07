# AI-Native Development Workflow

Hệ thống phát triển phần mềm hoàn toàn bằng AI Agent.

## Phase 1 - Bootstrap Project

Viết 1 prompt mô tả toàn bộ hệ thống.

**Ví dụ prompt:**

```
You are a senior software architect.
I want to bootstrap a full AI-native development repository.

Project idea:
A SaaS platform for managing study schedules for students.

Target users:
Students preparing for exams.

Core features:
- user authentication
- create study tasks
- scheduling
- progress tracking

Tech stack:
Frontend: Next.js + Tailwind
Backend: Node.js + Express
Database: PostgreSQL
ORM: Prisma
Auth: JWT

System requirements:
- scalable architecture
- REST API
- modular backend
- secure authentication
- mobile responsive UI

Please generate the entire repository structure including:
- ai-context/
- workflow/
- api/
- testing/
- agents/

Fill each markdown file with detailed content.
```

**Kết quả:** Agent tạo toàn bộ cấu trúc:
- [ai-context/](ai-context) - Context và kiến trúc hệ thống
- [workflow/](workflow) - Quy trình làm việc
- [api/](api) - Quy tắc API
- [testing/](testing) - Hướng dẫn testing
- [agents/](agents) - Specialized agents

## Phase 2 - Generate Features

Sau khi bootstrap xong, tạo feature specifications.

**Prompt:**

```
Create feature specifications for this product.

Generate specs for:
- authentication
- study tasks
- scheduling
- progress tracking
```

**Kết quả:** Agent tạo `spec/features/` với các file spec chi tiết.

## Phase 3 - UI Generation

Tạo UI prompts cho từng feature.

**Prompt:**

```
Generate UI prompts for each feature.
```

**Kết quả:** Agent tạo `ui/prompts/` chứa các file:
- login.md
- dashboard.md
- tasks.md

Sử dụng các prompt này với Stitch để generate UI.

## Phase 4 - Import UI

Sau khi Stitch export HTML, import vào project.

**Prompt:**

```
Convert these HTML files into React components
using Next.js and Tailwind.
```

**Input:** `ui/raw-html/`
**Output:** `src/frontend/components/`

## Phase 5 - Backend Generation

Generate backend dựa trên database design và API contract.

**Prompt:**

```
Based on:
- database design
- api contract

Generate backend implementation.
```

**Kết quả:** Agent tạo `src/backend/` với:
- controllers
- services
- routes

## Phase 6 - Agent Review

Chạy các agent review chuyên biệt.

**Prompt:**

```
Run architecture review
Run security review
Run performance review
```

**Agents:**
- [architect.md](agents/architect.md) - Review kiến trúc
- [security.md](agents/security.md) - Review bảo mật
- [performance.md](agents/performance.md) - Review hiệu năng

## Workflow Hoàn Chỉnh

```
IDEA
 ↓
Bootstrap prompt
 ↓
Agent generate dev system
 ↓
Feature specs
 ↓
UI prompts
 ↓
Stitch UI
 ↓
HTML import
 ↓
Frontend generation
 ↓
Backend generation
 ↓
Agent review
```

## Ưu Điểm

**Tốc độ cao:**
- Idea → Full repo structure: 30-60 giây
- Chỉ cần 1 prompt bootstrap + Copilot

**Tự động hóa:**
- Generate toàn bộ cấu trúc
- Generate code theo chuẩn
- Review tự động

## Nhược Điểm

**Phụ thuộc prompt:**
- Prompt không đủ chi tiết → Architecture sai
- Prompt không rõ ràng → API design sai
- Prompt thiếu constraints → DB design sai

**Giải pháp:** Prompt phải chứa đầy đủ:
- Product description
- Features list
- Tech stack
- Constraints
- Architecture preference

## Best Practice

Prompt bootstrap nên có 4 phần:

**1. Product**
```
Project idea: SaaS platform for managing study schedules
Target users: Students preparing for exams
```

**2. Features**
```
Core features:
- user authentication
- create study tasks
- scheduling
- progress tracking
```

**3. Tech Stack**
```
Frontend: Next.js + Tailwind
Backend: Node.js + Express
Database: PostgreSQL
ORM: Prisma
Auth: JWT
```

**4. Constraints**
```
Constraints:
- use REST API
- use service layer
- use Prisma migrations
- follow clean architecture
- implement error handling
- add input validation
```

Với 4 phần này, Agent sẽ generate code chuẩn và nhất quán.

## Tài Liệu Tham Khảo

- [AI Context](ai-context) - System architecture và business rules
- [Workflow](workflow) - Quy trình feature, bug, chore
- [API Guidelines](api) - Quy tắc endpoint
- [Testing](testing) - Backend, frontend, E2E testing