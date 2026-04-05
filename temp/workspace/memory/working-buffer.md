# Working Buffer (Danger Zone Log)

**Status:** ACTIVE  
**Started:** —  
**Context %:** —  

---

This file captures every exchange after context exceeds 60%. It survives compaction and is used for recovery.

**Protocol:** When `session_status` shows >60%, start logging each human message and your response summaries here.
