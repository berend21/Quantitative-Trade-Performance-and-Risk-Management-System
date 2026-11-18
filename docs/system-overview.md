# STS — System Architecture Overview

## System Description

STS (Smarter Trading Systems) is a self-hosted trading journal and quantitative performance analysis application designed to help traders measure, understand, and improve their trading process.

The application combines trade lifecycle management, quantitative performance analytics, risk evaluation, and qualitative trading reviews within a single application.

The central feedback loop is:

**Record → Measure → Review → Identify Patterns → Improve**

## Project Objectives

The system has five primary objectives:

- **Trade Lifecycle Management:** Record and maintain historical trading activity, including partial position closures.
- **Quantitative Performance Measurement:** Evaluate trading results using risk-normalized metrics.
- **Risk Analysis:** Understand the relationship between initial risk, realized outcomes, and drawdown.
- **Qualitative Review:** Associate trades with notes, screenshots, observations, and trading rules.
- **Continuous Improvement:** Identify recurring patterns and evaluate changes to trading behavior.

## Architectural Philosophy

STS follows a lightweight, feature-oriented monolithic architecture.

The application deliberately avoids unnecessary distributed infrastructure and microservice decomposition.

This architectural approach is based on the current application scope:

- Single-user application.
- Self-hosted deployment.
- Relatively low concurrency requirements.
- Strong transactional consistency requirements.
- Limited operational complexity.
- No demonstrated need for independently scalable services.

The objective is to maintain clear internal architectural boundaries while retaining the operational simplicity of a monolithic deployment.

## System Context

STS operates as a private application accessed through a web browser.

The user records trading activity, maintains journal entries, manages supporting material, and requests historical performance analysis.

```mermaid
flowchart TD
    User["Trader / Application Owner"]
    Browser["Web Browser"]
    STS["STS Application"]
    DB[("SQLite Database")]
    Files["Persistent File Storage"]

    User --> Browser
    Browser -->|"HTTP Requests"| STS
    STS -->|"Read / Write"| DB
    STS -->|"Upload / Retrieve"| Files
    STS -->|"HTML Responses"| Browser
