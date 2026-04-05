# MEMORY.md - Long-Term Memory

_This file stores curated memories, decisions, and insights worth keeping._

## Initial Setup

- **2026-03-24**: Workspace initialized. OpenClaw gateway restarted, configuration updated to show free models only in dropdown.
- **Persona**: Nex - Embedded AI assistant, concise, practical, professional âš?- **2026-03-25**: Proactive Agent v3.1.0 onboarding completed.
  - User X confirmed: name, timezone (GMT+8), communication style (direct), goals (explore interests, plan, make money), vision (family happiness), productivity peaks (morning/evening), async preference.
  - Context updated in USER.md: full-house customization designer, wife and son, serious personality.
  - SOUL.md adjusted: professional, precise, no fluff.
  - Protocols active: WAL, Working Buffer, Compaction Recovery, Autonomous Crons.

## Installed Skills

- **skill-vetter** v1.0.0 - Security vetting tool
- **self-improving-agent** v3.0.6 (@pskoett, 301k downloads) - Continuous learning system
- **agent-browser** v0.2.0 (@thesethrose, 167k downloads) - Headless browser automation
  - Chrome for Testing manually downloaded to `C:\chrome-for-testing\chrome-win64\`
  - Environment variable: `AGENT_BROWSER_EXECUTABLE_PATH` set to Chrome binary
  - Skill installed with `--force` after reviewing SKILL.md (no malicious code detected)
- **proactive-agent** v3.1.0 (@halthelobster, 120k downloads) - Proactive agent architecture
  - Deployed assets: ONBOARDING.md, HEARTBEAT.md (not overriding existing AGENTS.md, USER.md, SOUL.md)
  - Protocols: WAL, Working Buffer, Compaction Recovery, Autonomous Crons

## Preferences

- **ClawHub æœç´¢è®¾ç½®**: æŸ¥æ‰¾åº”ç”¨æ—¶ï¼Œä¸è¦å‹¾é€?"Hide suspicious"ï¼ˆéšè—å¯ç–‘ï¼‰é€‰é¡¹ï¼Œä»¥æŸ¥çœ‹å®Œæ•´æŠ€èƒ½åˆ—è¡¨ï¼ŒåŒ…æ‹¬æ‰€æœ‰è¯„åˆ†å’Œé€‰é¡¹ã€?- **æŠ€èƒ½å®‰è£…ç­–ç•?*: ä¼˜å…ˆå®‰è£…é«˜ä¸‹è½½é‡ã€é«˜è¯„åˆ†çš„å®˜æ–¹æˆ–çŸ¥åä½œè€…æŠ€èƒ½ã€‚å®‰è£…å‰ä½¿ç”¨ skill-vetter è¿›è¡Œå®‰å…¨å®¡æŸ¥ã€?- **è‡ªæˆ‘æ”¹è¿›**: å·²é…ç½?self-improving-agent v3.0.6ï¼Œä½¿ç”?`.learnings/` Markdown æ ¼å¼è®°å½•å­¦ä¹ ã€?- **æµè§ˆå™¨è‡ªåŠ¨åŒ–**: ä½¿ç”¨ agent-browserï¼Œéœ€ç¡®ä¿ Chrome for Testing è·¯å¾„é…ç½®æ­£ç¡®ã€?
## Important Context

_Keep track of important people, projects, and recurring tasks here._

---

_This file is updated periodically during heartbeat checks and significant events._

## 2026-03-28 - OpenClaw ±¸·ÝÏµÍ³

- ? SSH ÃÜÔ¿ÒÑÉú³É²¢Ìí¼Óµ½ GitHub£¨Ed25519£©
- ? Ë½ÓÐ²Ö¿â `my-openclaw-backup` ÒÑÅäÖÃ²¢²âÊÔÁ¬½Ó
- ? ´´½¨ÊÖ¶¯±¸·Ý½Å±¾ `openclaw-config-backup.ps1`£º
  - ½ö±¸·Ý¹Ø¼üÅäÖÃºÍ¼ÇÒä£¨ÅÅ³ý extensions/¡¢sandboxes/¡¢node_modules/£©
  - °üº¬£ºopenclaw.json, config.json, config.yaml, identity/, devices/, cron/, memory/, workspace/memory/, workspace/*.md
  - Ìå»ý ~30KB£¬Ô¶µÍÓÚ GitHub 100MB ÏÞÖÆ
- ? ´´½¨»Ø¹ö½Å±¾ `restore-openclaw-config.ps1`£º
  - Í£Ö¹ gateway ¡ú ½âÑ¹±¸·Ý ¡ú ÖØÆô ¡ú ÑéÖ¤
  - ×Ô¶¯±¸·Ýµ±Ç°×´Ì¬ºóÔÙ»Ø¹ö
- ? PowerShell ±ðÃûÓÀ¾ÃÉèÖÃ£º`boc`£¨±¸·Ý£©¡¢`roc`£¨»Ø¹ö£©

## 2026-03-28 - OpenClaw Backup System

**Goal:** Configure OpenClaw automatic backup to private GitHub repository for safe configuration rollback capability.

**Key Decisions:**
- Use Ed25519 SSH keys for GitHub authentication
- Manual PowerShell scripts instead of openclaw backup (due to size limitations and filtering constraints)
- Include only configuration and memory files (~30KB), exclude extensions/node_modules (~180MB)
- Create both backup and restore scripts with safety checks
- Add PowerShell aliases (oc, oc) to profile for convenience

**Implementation:**

### SSH Configuration
- Generated Ed25519 key pair (~\.ssh\id_ed25519)
- Added public key to GitHub account
- Verified connection: ssh -T git@github.com successful

### Repository Setup
- Created local backup directory: C:\Users\Administrator\openclaw-backups`n- Initialized git and added remote: git@github.com:wang4869527/my-openclaw-backup.git`n- Initial full backup attempt failed (179MB > 100MB GitHub limit)

### Manual Backup Script: openclaw-config-backup.ps1`n- Copies essential files to temp directory:
  - openclaw.json, config.json, config.yaml`n  - identity/, devices/, cron/`n  - memory/ + memory/self-improving/`n  - workspace/memory/`n  - workspace/*.md (AGENTS.md, HEARTBEAT.md, MEMORY.md, TOOLS.md)
- Creates tar archive (~30KB)
- Commits and pushes to GitHub

### Restore Script: estore-openclaw-config.ps1`n- Automatically backs up current state before restore (to efore-restore branch)
- Stops OpenClaw gateway (checks scheduled task, service, process)
- Extracts and overwrites files
- Restarts gateway
- Prompts to run openclaw config validate and test; if issues, run oc to rollback

### Git History Cleanup
- First push contained large objects, causing git push failure
- Solution: deleted .git, re-initialized, added only small backup files, force-pushed

### PowerShell Aliases
Added to $profile:
- oc - run backup script
- oc - run restore script

### Verification Workflow
1. oc`n2. Modify configuration
3. openclaw config validate`n4. openclaw gateway restart`n5. Test; if fails, run oc to rollback

**File Locations:**
- Backup script: C:\Users\Administrator\openclaw-config-backup.ps1`n- Restore script: C:\Users\Administrator\restore-openclaw-config.ps1`n- Backup directory: C:\Users\Administrator\openclaw-backups\`n- Git remote: origin git@github.com:wang4869527/my-openclaw-backup.git`n
**Learnings:**
- OpenClaw's built-in ackup create lacks fine-grained filtering; --no-include-workspace still includes extensions/node_modules (~180MB)
- Always test restore process after setting up backup
- Git history cleanup (removing large files) requires fresh repository init
- PowerShell profile aliases streamline safety-critical workflows

**Next Steps:**
- Consider setting up Windows Task Scheduler for daily automatic oc`n- Implement retention policy (keep last 5 backups) to avoid repo bloat
- Test full restore from scratch to validate disaster recovery procedure

## 2026-03-30 - Configuration Recovery & Maintenance Learnings

- **Exec Host Configuration Issue**: Discovered 	ools.exec.host misconfigured (set to gateway instead of sandbox), causing shell command execution failures. Resolved by correcting configuration. Key lesson: validate exec host settings after any system changes affecting tool execution.
- **Disk Space Management Strategy**: Created comprehensive C drive cleanup plan (~15GB target):
  - Package manager caches: pnpm (~2GB), npm (~1.75GB), yarn/npm global
  - Docker resources: docker system prune -a (unused images/containers/volumes) ~2-3GB
  - NVIDIA driver caches: ~1-2GB
  - Application caches: WeChat, QQ, WPS, Chrome, Edge ~3-4GB
  - Log rotation: retain last 7 days, delete older logs
  - Risk controls: verify app not in active use, preserve config files, perform category-by-category review before deletion
- **Pending Infrastructure Tasks**: 1Panel (Docker-based), enable sandbox mode (gents.defaults.sandbox.mode=non-main), install OpenRouter skill plugin.

**Proactive Idea**: Build Bitable project pipeline tracker for full-home customization projects to visualize client journey, automate follow-ups, and improve milestone tracking. Aligns with user's business needs and goal to "make money".


## 2026-03-30 - Daily Summary

**Highlights:**
- Fixed exec misconfiguration (tools.exec.host=gateway)
- Completed disk cleanup: freed ~13GB (NVIDIA, Google, Tencent, WPS, npm, Docker caches)
- Configured automatic backup (Scheduled Task: daily 3am)
- Enabled OpenClaw UI access (fixed control-ui path)
- Disabled sandbox mode (deferred per user request)
- Disabled obsolete 'OpenClaw Node' scheduled task
- Tried installing free-models-for-openclaw (ClawHub 429 limit ¡ú manual copy not recognized)

**Issues Encountered:**
- Chrome lost passwords due to sync being paused (data intact, recoverable)
- ClawHub rate limit blocked skill install
- Gateway restart loops due to plugin config mismatch (resolved)
- C drive space repeatedly low (6GB currently)

**Pending Tasks:**
- Enable 1Panel (requires Docker start)
- Enable sandbox mode
- Install OpenRouter skill plugin (or wrap free-models-for-agent library)
- Regular disk cleanup scheduling

**Learnings:**
- Config changes require gateway restart; mismatched plugin names cause restart loops
- Chrome sync status affects password visibility (file not deleted)
- ClawHub limits may require waiting or manual install

