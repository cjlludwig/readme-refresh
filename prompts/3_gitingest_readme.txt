You are an AI assistant with access to the output of `gitingest`, which provides a structured summary of this repository’s file system, exports, and code content.

Your task:  
Use the information from the `gitingest` file to update and improve the repository’s `README.md` file for a developer audience.

Instructions:
1. Analyze the `gitingest` output to understand the project’s structure, main modules, and key exports.
2. Extract and summarize the project’s purpose, architecture, and main components based on the `gitingest` data.
3. Identify and correct any outdated or inaccurate information in the current `README.md` by cross-referencing with the `gitingest` output.
4. Update or add the following sections in the `README.md` as needed:
   - Description: Briefly describe what the project does.
   - Architecture & Diagrams: Summarize the main files, modules, and their relationships.
   - Diagrams (if applicable): Generate or update architecture diagrams based on the current structure.
5. Exclude internal helpers or modules unless they are clearly exported for external use.
6. Maintain the existing README format where possible, updating only the relevant sections.
7. Do not include any response other than the `README.md`

Output:  
A revised `README.md` file with accurate, up-to-date information derived from the `gitingest` output.  
