# Requirements – Sahayak AI

## Problem Statement
Citizens struggle to discover and understand government schemes they may be eligible for due to fragmented information sources, complex eligibility rules, and language barriers.

## Objective
Build an AI-powered, eligibility-first platform that helps users discover relevant government schemes and clearly understand why they may qualify, with a strong focus on inclusion and accessibility.

## Target Users
- Underserved and low-awareness citizens
- First-time government scheme applicants
- Users with language or digital literacy barriers

## In Scope
- Anonymous-first usage
- Session-based eligibility checking using minimal user inputs
- AI-assisted understanding of user inputs
- Clear, human-readable eligibility explanations
- Multilingual support (maximum 2 languages)
- Optional user opt-in for future alerts
- Official scheme links and document requirements

## Out of Scope
- Scheme application submission or tracking
- Guaranteed eligibility confirmation
- Aadhaar or sensitive personal data collection
- Medical or financial advice
- Full nationwide or all-state coverage beyond MVP

## Functional Requirements
- Collect minimal user inputs during a single interaction session
- Match user inputs against predefined eligibility rules
- Suggest relevant government schemes
- Explain eligibility reasoning in simple language
- Provide official sources and application links for each scheme

## Non-Functional Requirements
- High availability using a serverless architecture
- Low-latency responses suitable for real-time interaction
- Privacy-first and consent-driven design
- Scalable and extensible system architecture
- Explainable and responsible AI usage

## Constraints
- No official government APIs assumed
- Scheme information accuracy limited to last update
- Eligibility results are advisory, not authoritative
- AI responses constrained to curated data sources
- Scheme data curated and maintained manually for MVP
- Internet connectivity required for core functionality

## Success Criteria
- Users can discover relevant schemes in under 2 minutes
- Eligibility explanations are clear and understandable
- System avoids false guarantees or misleading claims
