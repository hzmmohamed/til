---
draft: true
---
Anatomy of a dropzone file input:
1. No component state. The state is managed directly by react hook form
2. onDrop: set the value of the react-hook-form state
3. The file delete handler edits the value of the field in the form state

types of errors in a file input using dropzone:
- Rejected files due to size or file type
- Other validation rules (they are at the form level, not the file input level)

Validating:

UI:
1. Empty state
2. Partially filled state
3. Completely filled state
4. Read only state
5. 
