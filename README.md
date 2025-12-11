                                             AI Construction Safety Inspector
  An end-to-end automation system for real-time safety compliance detection in construction site photographs, leveraging Gemini Vision AI and n8n for instant analysis and alerting.

                                                       Overview
  The AI Construction Safety Inspector automates the critical task of site safety auditing. Users upload construction images via the Lovable frontend, triggering a 10-node automation workflow. The system instantly analyzes worker compliance (helmets, vests, harnesses) and generates a structured safety score and summary. If the safety score drops below 80, an immediate email alert is dispatched to supervisors. All results are logged in Supabase for historical tracking and compliance reporting.
This solution removes the dependency on manual, time-consuming inspections, making safety monitoring immediate and data-driven.

                                                       Key Features
**Real-time Image Analysis**: Instant safety violation detection upon image upload.

**Gemini Vision Integration**: Uses the Gemini API for highly accurate, complex visual analysis of safety compliance.

**Critical Alerting**: Automatic Gmail/SMTP notifications for scores below the safety threshold (< 80).

**Structured Output**: Generates a precise JSON report including counts for:
total_workers
without_helmet
without_vest
unsafe_ladders
harness_issues
safety_score

**Data Persistence**: All analysis logs, scores, and image metadata are stored in a Supabase Postgres database.

**Scalable Architecture**: Designed for easy transition from manual uploads to continuous live camera feed processing.

                                                System Architecture & Workflow
The system is orchestrated by a single, sequential 10-node n8n workflow.

**Image Upload**: User uploads photo via the Lovable frontend, triggering the Webhook.

**File Handling**: Image is processed, renamed, and uploaded to the Supabase Storage Bucket.

**AI Analysis**: The image URL is sent to the Gemini Vision API with a strict JSON-output prompt.

**Response & Clean-up**: The webhook confirms receipt. A Code Node (Java) cleans the Gemini JSON response to ensure data integrity.

**Data Storage**: Cleaned results are inserted into a Supabase Postgres Table.

**Conditional Alert**: An IF Node checks if Safety Score < 80.

**Notification**: If true, a critical alert is sent via the Send Gmail Node.

                                                     Technical Stack

The core system is built on an affordable, robust, and scalable stack:

**Automation**: n8n serves as the main workflow orchestrator and API glue, managing the entire 10-node pipeline.

**Vision AI**: Gemini (Vision API) is the core intelligence layer, performing the safety analysis and detection logic with high precision.

**Database & Storage**: Supabase is utilized for both structured and unstructured data:

**Supabase Postgres** for structured storage of all safety logs, scores, and timestamps.

**Supabase Storage** for object storage of the raw uploaded image files.

**Frontend/PDF**: Lovable provides the user interface for image uploads and handles the external generation of final PDF reports.

**Alerting**: Gmail / Google SMTP is used to provide instant, reliable notification for all critical safety violations.


                                                    Setup & Deployment
**Supabase Setup**: Provision a new Supabase project, create the necessary safety_logs table (refer to project documentation for schema), and set up a Storage Bucket.

**Gemini API Key**: Obtain and secure your Gemini API Key in n8n's credentials.

**n8n Workflow**: Import the 10-node workflow file. Configure the HTTP Node (Supabase upload endpoint) and the Gmail Node credentials.

**Webhook Integration**: Expose the n8n Webhook URL and configure it as the target endpoint in your Lovable application.

                                                   Future Enhancements
The current architecture provides a highly stable foundation that is ready for significant scaling:

**Live Feed Integration**: Replace manual uploads with direct integration to live camera feeds for continuous, automated monitoring.

**Advanced Analytics Dashboard**: Develop a dedicated frontend dashboard pulling data from Supabase for real-time safety trends and predictive analysis.

**Multi-Site Management**: Expand the database schema and frontend to support logging and reporting across multiple construction locations.

**Refining AI Logic**: Introduce detection for additional hazards such as debris and blocked walkways.

