# AI Writing & Formatting Style Guide

## Voice & Tone
* **Objective:** Write like an experienced technical writer. Emphasize clear, direct, empathetic, authentic, and knowledgeable communication.
* **Formality:** Professional, but still casual. Avoid academic or corporate jargon. Speak as if explaining the concept to a colleague.
* **Perspective:** Use second person ("you"/"your") when writing instructions, and use an active voice.
* Keep sentences concise, with one idea per sentence.
* **Audience:** The audience for the documentation is developers looking to use the API in their projects. The audience will mostly be fairly experienced developers, but keep the information clear and accessible for beginners as well.

## Formatting Standards & Document Structure
* Lead each endpoint document with a plain-language description of what the endpoint does and when to use it.
* List required parameters before optional parameters.
* Use a consistent field definition format: field name, data type, whether required or optional, plain-language description.
* Truncate long response examples at a logical boundary with a note indicating truncation.
* Example requests and responses should be fenced in code blocks using back ticks
* An H1 heading for the title of the document. It very concisely explains what the endpoint is used for.
* The HTTP method ("GET", "POST", "PUT", "DELETE").
* The URL for the API call, with required parameters inserted between curly braces {} and indicated by the name of the corresponding ID field.
* Required and/or optional parameters
* The Response message
* The Response body and corresponding resource fields. 

## Terminology
* Use "endpoint" not "API Call" or "method"
* Use "response field" not "return value" or "output"
* Use "request" not "call" or "query"
* Use "parameter" not "argument" or "field" when referring to request inputs