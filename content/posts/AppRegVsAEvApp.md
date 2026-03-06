+++
title = "App Registration vs Enterprise Application "
date = 2026-03-06
description = "Understand the difference between App Registrations and Enterprise Applications in Microsoft Entra ID."
[taxonomies]
tags=["EntraID","Azure","Identity"]
+++

{% tldr() %}
**Don't want the long explanation?**

An **App Registration** is the **application definition**.

An **Enterprise Application** is the **instance of that application inside a tenant**.

Every App Registration automatically creates an Enterprise Application in the same tenant.

Think of it like:

- App Registration → the **blueprint**
- Enterprise Application → the **installation**
{% end %}

------------------------------------------------------------------------

## The problem

<img src="/images/doh.gif"
     style="float:right;width:260px;margin:0 0 1rem 1.5rem;border-radius:6px;">

If you've spent more than **five minutes** inside Microsoft Entra ID,  
you've probably seen these two menus:

- **App registrations**
- **Enterprise applications**

And at some point you probably asked yourself:

> Why are there two things that look like the same thing?

You create an app.

Then suddenly you see **another app with the same name somewhere else**.

Did Azure duplicate it?  
Did someone clone it?  
Did you break something?

No.

You're just looking at **two different perspectives of the same application**.

<div style="clear: both;"></div>

------------------------------------------------------------------------

## The short explanation

The easiest way to think about it:

| Thing | What it represents |
|-----|-----|
| **App Registration** | The **application definition** |
| **Enterprise Application** | The **application inside a tenant** |

Or more technically:

| Object | Entra ID terminology |
|-----|-----|
| App Registration | **Application Object** |
| Enterprise Application | **Service Principal** |

In simple terms:

- **App Registration** → describes the application
- **Enterprise Application** → represents the application **inside a tenant**

One application definition can exist in **many tenants**.

Each tenant gets its **own Enterprise Application**.

------------------------------------------------------------------------

## Visual explanation

This relationship becomes much clearer visually.

{% mermaid() %}
graph LR

    A[App Registration<br>Application Object]
    B[Enterprise Application<br>Service Principal<br>Tenant A]
    C[Enterprise Application<br>Service Principal<br>Tenant B]
    D[Enterprise Application<br>Service Principal<br>Tenant C]

    A --> B
    A --> C
    A --> D

    style A fill:#DF6155,stroke:#333,stroke-width:2px,color:#fff
    style B fill:#e6f3ff,stroke:#333
    style C fill:#e6f3ff,stroke:#333
    style D fill:#e6f3ff,stroke:#333
{% end %}

What happens here:

1. A developer creates **one App Registration**
2. When the application is used in a tenant
3. Azure creates a **Service Principal**
4. That Service Principal appears as an **Enterprise Application**

So the same application can appear in **many tenants at once**.

------------------------------------------------------------------------

## What actually happens when you create an app

When you click **New registration** in Entra ID, this is what really happens:

{% mermaid() %}
graph LR

    A[Developer creates App Registration]
    B[Application Object created]
    C[Service Principal created]
    D[Enterprise Application appears in tenant]

    A --> B --> C --> D

    style B fill:#DF6155,stroke:#333,color:#fff
{% end %}

Meaning:

Every **App Registration automatically creates a Service Principal in the same tenant**.

That Service Principal is what you see as an **Enterprise Application**.

Which is why you suddenly see **two objects with the same name**.

They're supposed to exist.

------------------------------------------------------------------------

## Why Microsoft separated these two things

Because an **application definition** and a **tenant configuration** are different problems.

| Layer | Example settings |
|-----|-----|
| **App Registration** | Redirect URIs, certificates, API permissions |
| **Enterprise Application** | User assignments, Conditional Access, SSO |

So typically:

- **Developers manage App Registrations**
- **Administrators manage Enterprise Applications**

Two roles.  
Two interfaces.

One application.

------------------------------------------------------------------------

## Where confusion usually happens

Most confusion appears when troubleshooting authentication.

Typical questions:

> "Why do I see the app twice?"

Because one is the **definition** and the other is the **instance**.

> "Where do I assign users?"

Enterprise Application.

> "Where do I configure Conditional Access?"

Enterprise Application.

> "Where do I configure API permissions?"

App Registration.

Once you know this split, the portal suddenly makes a lot more sense.

------------------------------------------------------------------------

## A real world analogy

Imagine a **software product**.

| Concept | Real world analogy |
|-----|-----|
| App Registration | The **software blueprint** |
| Enterprise Application | The **installation on a server** |

You can have:

- One blueprint
- Many installations

Exactly like applications across tenants.

------------------------------------------------------------------------

## Final thought

The Entra portal makes this feel confusing.

But the mental model is actually simple.

```
App Registration = The application definition
Enterprise Application = The application inside your tenant
```

Or in Entra ID terms:

```
Application Object = App Registration
Service Principal = Enterprise Application
```

Once you see it that way, the whole identity model suddenly makes a lot more sense.

And those **two mysterious menus** stop feeling mysterious.