# ai-gm-core API (Draft)

> This document is **not a formal API specification**.
> It describes the intended role and minimal interface of ai-gm-core
> as an AI Game Master core.
>
> Endpoints, parameters, and formats are expected to evolve.

---

## Purpose

This API defines the minimal interface for interacting with **ai-gm-core**.

Its role is simple:

* Receive **player behavior logs**
* Interpret them through an AI Game Master
* Return **world consequences as narrative text**

This is **not** a game server API.
It is an interface to a *thinking component*.

---

## What This API Is Not

* No authentication
* No authorization
* No security guarantees
* No monetization assumptions
* No real-time synchronization

Those concerns belong **outside** ai-gm-core.

---

## Core Philosophy

* Players do not send commands
* Behavior itself becomes the prompt
* No correctness judgment
* The world progresses asynchronously

The API exists to support **narrative causality**, not mechanics.

---

## Intended Clients

* Game engines (Unreal, Unity, etc.)
* CLI tools
* Text-based experimental clients
* Manual `curl` requests

If it can be called with `curl` and returns a narrative,
it is considered sufficient.

---

## Conceptual Endpoint Example

### POST /gm/observe

Submit player behavior to the AI Game Master.

#### Request (Conceptual)

* `world_id`
* `session_id`
* `player_action_log`
* Optional metadata

The exact structure is intentionally undefined.

ai-gm-core is responsible for **interpreting**, not validating, behavior.

---

### player_action_log May Include

* Actions taken
* Actions not taken
* Hesitation or indecision
* Repeated avoidance
* Silence or non-intervention

All of these are meaningful inputs.

---

### Response (Conceptual)

* `narrative`
* Optional `world_delta`
* Optional notes or hints

The response does **not** include:

* Success / failure flags
* Scores
* Win / lose conditions

It describes **how the world changed**.

---

## World Context Handling

Worldviews and settings are not mandatory API inputs.

ai-gm-core selectively assembles the required context internally,
based on the received behavior.

For details, see `README_jp.md`
(section: *Handling Worldviews and Settings*).

---

## Design Constraints

* Do not rely on future LLM capabilities
* Prefer minimal, energy-efficient context
* Optimize for plausibility over completeness
* Keep the interface small and flexible

---

## Role of This Document

This file exists to:

* Share intent
* Provide a discussion anchor
* Clarify what is *not* fixed yet

The API may change.

**The idea should remain.**
