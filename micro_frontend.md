## 1. What is a Micro Frontend?

Answer:
A Micro Frontend is an architectural approach where a frontend
application is split into smaller, independently developed, tested, and
deployed applications.

Example:

-   Team A → Authentication

-   Team B → Dashboard

-   Team C → Payments

-   Team D → Profile

Each team owns its own frontend.

## 2. Why use Micro Frontends?

Benefits:

-   Independent deployment

-   Smaller codebases

-   Team autonomy

-   Easier maintenance

-   Technology flexibility (React, Vue, Angular together)

-   Faster development

## 3. What are the disadvantages?

-   Larger bundle size

-   Shared dependency management

-   Routing complexity

-   State sharing challenges

-   Performance overhead

-   Version conflicts

## 4. Different ways to implement Micro Frontends?

> Common approaches:
>
> **Build-time Integration**
>
> Combine apps during build.
>
> Example:
>
> npm package
>
> **Runtime Integration**
>
> Load applications dynamically.

Example:

-   Module Federation

-   Single SPA

-   iframe

**Server-side Composition**

Compose pages on the server before sending HTML.

Edge-side Includes

Compose at CDN/Edge.

## 5. What is Module Federation?

One of **Webpack 5\'s** biggest features.

It allows one application to **expose** **modules** that another
application can load at runtime without rebuilding.

## 6. Explain Host and Remote.

Host

Consumes remote applications.

Remote

Exposes components/modules.

## 7. How do applications communicate?

Methods:

-   Props

-   Custom Events

-   Redux

-   Context API

-   RxJS

-   Event Bus

-   Browser Storage

-   URL Parameters

## 8. How do you share authentication?

Usually:

-   JWT Token

-   Cookies

-   Shared Auth Service

-   OAuth Provider

## 9. How do you share state?

Options:

-   Redux

-   Zustand

-   Context

-   Event Bus

-   Shared Library

## 10. Challenges in Micro Frontends


-   Duplicate React versions

-   CSS conflicts

-   Shared dependencies

-   Routing

-   SEO

-   Authentication

-   Error boundaries

11. How do you avoid CSS conflicts?

Methods:

-   CSS Modules

-   Tailwind CSS

-   Styled Components

-   Shadow DOM

-   Naming conventions (BEM)



# Microfrontends

## What are Microfrontends?

Microfrontends extend the microservices concept to the frontend by splitting a large application into independently developed, deployed, and maintained frontend modules.

### Benefits

- Independent deployments
- Team autonomy
- Technology flexibility
- Better scalability
- Smaller codebases

### Common Approaches

- Webpack Module Federation
- Single-SPA
- iframes (legacy)
- Web Components

### Interview One-Liner

> **Microfrontends allow multiple teams to independently build, deploy, and maintain different parts of a large frontend application while presenting a unified user experience.**

# Microfrontends

## What are Microfrontends?

Microfrontends extend the **microservices architecture** to the frontend by breaking a large application into **independently developed, deployed, and maintained frontend modules**, each owned by a separate team.

Each microfrontend is responsible for a specific business domain while providing a seamless user experience.

---

## Benefits

- Independent deployments
- Team autonomy
- Technology flexibility
- Better scalability
- Faster development cycles
- Easier maintenance

---

## Challenges

- Shared dependencies
- Design consistency
- Communication between applications
- Routing coordination
- Authentication and authorization
- Performance overhead

---

## Common Tools

- Webpack Module Federation
- Single-SPA
- Web Components
- iframes (legacy approach)

---

## Interview One-Liner

> **Microfrontends allow multiple teams to independently build, deploy, and maintain different parts of a frontend application while presenting a unified user experience.**

---
