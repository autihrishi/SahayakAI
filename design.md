# Design – Sahayak AI

## Overview
Sahayak AI is an eligibility-first, AI-assisted platform designed to help citizens discover and understand government schemes they may qualify for. The system prioritizes accessibility, correctness, and responsible AI usage.

The design intentionally separates deterministic eligibility logic from AI-based language understanding and explanation.

---

## High-Level Architecture

Frontend:
- Flutter Web application
- Anonymous-first interaction
- Text-first with optional voice support

Backend:
- AWS API Gateway
- AWS Lambda (serverless functions)

AI & Language Services:
- Amazon Bedrock (LLM-based language understanding and explanation)
- Amazon Transcribe (Speech-to-Text, bilingual)
- Amazon Polly (Text-to-Speech)

Data Store:
- DynamoDB (scheme metadata and eligibility rules)

Authentication (Optional):
- AWS Cognito (opt-in only)

---

## Component Breakdown 

### Frontend
- Collects minimal user inputs during a single session
- Supports text input and optional voice input
- Displays eligibility results and explanations
- Does not store sensitive user data locally

### Backend APIs
- `/parse-input`: Uses Amazon Transcribe (for voice) and Amazon Bedrock to normalize user input into structured form
- `/check-eligibility`: Evaluates structured input against eligibility rules
- `/explain-result`: Uses Amazon Bedrock to generate human-readable explanations
- `/tts-response`: Uses Amazon Polly to generate voice output from text explanations

### Eligibility Engine
- Rule-based and deterministic
- Uses predefined eligibility criteria stored in the database
- Produces auditable and explainable outcomes
- No AI-based decision making at this layer

### AI Layer (Amazon Bedrock)
Used strictly for:
- Interpreting free-form or ambiguous user inputs
- Generating clear, human-readable eligibility explanations
- Multilingual text generation
- Assisting offline conversion of unstructured scheme documents into structured rules

AI does not make eligibility decisions.

---

## Speech & Language Support

- Speech-to-Text (STT):
  - Implemented using Amazon Transcribe
  - Limited to **bilingual support** (English + Hindi) for MVP

- Text Processing & Explanation:
  - Implemented using Amazon Bedrock
  - Supports **multilingual text output**

- Text-to-Speech (TTS):
  - Implemented using Amazon Polly
  - Generates voice responses for eligibility explanations

Text input and output always remain available as a fallback to ensure reliability.

---

## Data Model (Conceptual)

Scheme Record:
- Scheme Name
- Scheme Type
- Applicable State (Central or State Name)
- Eligibility Rules (Structured JSON)
- Benefits Description
- Short Scheme Description
- Required Documents
- Official Application Link
- Application Mode (Online / Offline / Both)
- Scheme Status (Active / Inactive / Announced)
- Source Authority (e.g. Ministry of Health & Family Welfare, Government of Maharashtra)
- Last Updated Timestamp

User Session Data:
- State
- Gender
- Disability Status (Yes / No)
- Caste Category
- Age Range
- Income Range
- Occupation Category (Govt / Private Sector)
- Employment Type (Salaried / Self-employed / Unemployed / Student / Retired)
- Family Status (Married / Unmarried / Widowed)
- Number of Dependents (Parents, Children)
- Housing Status (Own / Rented)
- Vehicle Ownership (None / Two-wheeler / Four-wheeler)

User session data is not persisted by default.

---

## Data Flow

1. User provides inputs via text or voice on the frontend
2. Voice input is converted to text using Amazon Transcribe
3. Backend normalizes inputs using Amazon Bedrock
4. Eligibility engine evaluates rules from DynamoDB
5. Backend requests explanation from Amazon Bedrock
6. Optional voice output generated using Amazon Polly
7. Results returned to frontend for display

---

## Security & Privacy Considerations
- Anonymous-first design
- No Aadhaar or sensitive personal data collected
- Optional authentication only with explicit user consent
- No user data used to train AI models
- AI responses constrained to curated scheme data

---

## Scalability
- Stateless serverless backend
- Config-driven scheme rules
- Easy onboarding of new schemes without code changes

---

## Trade-offs & Limitations
- Manual scheme data curation for MVP
- Limited scheme coverage to ensure accuracy
- Internet connectivity required for AI and voice features
- Advisory-only eligibility results

---

## Future Enhancements
- Push-based scheme awareness for opted-in users
- Additional language support for speech input
- Integration with official government APIs if available
