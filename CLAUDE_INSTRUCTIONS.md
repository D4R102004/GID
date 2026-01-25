# GID PROJECT - INSTRUCTIONS FOR CLAUDE

## FOR YOU (THE USER) - HOW TO AVOID ERRORS ON YOUR PART

### 1. **Character Profile Headers - Use a Template**
Every character profile should start with this exact format:

```markdown
# **[CHARACTER NAME] - COMPLETE CHARACTER PROFILE**

## **BASIC INFO**

**Full Name:** [Full name]
**Nickname/Codename:** [If applicable]
**Age:** [EXACT age, not ranges] (Arc [number])
**Occupation:** [Current occupation]
**Status:** [Protagonist / Supporting / Antagonist]
**Family:** [Key family members]
```

**Why:** This forces you to fill in exact ages, prevents "TBD" accumulation, and helps Claude identify character roles immediately.

---

### 2. **Add Role Tags to Existing Files**
Go through your current character profiles and add this to the top:

```markdown
---
ROLE: Protagonist / Supporting / Antagonist
FACTION: Pristania / Free / Jitsumoto / None
STATUS: Alive / Dies Arc X
AGE_ARC_1: [number]
---
```

**Why:** Claude can scan these tags instantly without reading full files.

---

### 3. **Create a CHANGELOG.md**
Every time you update character info, log it:

```markdown
# GID LORE CHANGELOG

## 2025-01-26
- CHANGED: Yonoa's age from TBD → 33 (corrected in profile)
- CHANGED: Ichiro's occupation from TBD → Shopkeeper & Stage Magician
- ADDED: Verification that Kamigami are THREE children, not four
- CORRECTED: Glayne dies Arc 5, not Arc 1

## 2025-01-20
- ADDED: Cristopher's age confirmed as 25
- etc.
```

**Why:** Helps both of us track what's been changed and prevents reverting to old errors.

---

### 4. **Flag [TBD] Items in a Separate File**
Create **DEVELOPMENT_QUEUE.md**:

```markdown
# THINGS TO DETERMINE

## HIGH PRIORITY (Needed for current writing)
- [ ] Goro's exact Nouryoku name
- [ ] How Glayne discovers island location

## MEDIUM PRIORITY (Needed for Arc 3+)
- [ ] Hirohiko's specific Arc 3 role

## LOW PRIORITY (Arc 5+)
- [ ] Post-story fates
```

**Why:** Keeps [TBD] items visible and organized, prevents them from hiding in character profiles.

---

### 5. **Verify Cross-References**
When you mention a character in another character's profile, double-check:

**Example:** If you write "Tairin is one of the Kamigami" in Perlereina's profile, go to:
1. GID_MASTER_LORE.md → Check who the Kamigami actually are
2. Tairin's profile → Verify her faction/family

**Why:** Prevents contradictions from spreading across files.

---

## FOR CLAUDE - MANDATORY RULES TO AVOID ERRORS

### **RULE 1: READ FIRST, WRITE SECOND**
**NEVER make claims about characters without reading their profile first.**

```markdown
BAD:
User: "Tell me about Yonoa's age"
Claude: "Yonoa's age is TBD" [WRONG - didn't check]

GOOD:
User: "Tell me about Yonoa's age"
Claude: [calls view tool on YONOA_HOUZU_CHARACTER_PROFILE.md]
Claude: "Yonoa is 33 years old, the oldest of the five protagonists."
```

---

### **RULE 2: PROJECT KNOWLEDGE SEARCH IS FOR FINDING FILES, NOT FACTS**
Use `project_knowledge_search` to **locate which file to read**, then use `view` to **verify the fact**.

```markdown
BAD:
User: "Who are the Kamigami?"
Claude: [searches, sees fragments mentioning Tairin near Kamigami]
Claude: "The Kamigami are Perlereina, Tairin, Diominiciel, Hirohiko" [WRONG]

GOOD:
User: "Who are the Kamigami?"
Claude: [searches "Kamigami children Kami"]
Claude: [sees GID_MASTER_LORE.md in results]
Claude: [calls view on GID_MASTER_LORE.md lines 95-115]
Claude: "The Kamigami are Kami's THREE children: Diominiciel (eldest), Hirohiko (middle), Perlereina (youngest). Born ~35 years before Arc 1."
```

---

### **RULE 3: NEVER HALLUCINATE OCCUPATIONS, RELATIONSHIPS, OR PLOT POINTS**
If you don't know something, SAY "Let me verify that" and look it up.

```markdown
BAD:
User: "What does Ichiro do?"
Claude: "Ichiro is a chocolatier at Free HQ" [HALLUCINATION]

GOOD:
User: "What does Ichiro do?"
Claude: "Let me check his profile."
Claude: [calls view on ICHIRO_KIRYUIN_CHARACTER_PROFILE.md]
Claude: "Ichiro is a shopkeeper and stage magician at Free HQ."
```

---

### **RULE 4: CROSS-REFERENCE AGES WITH TIMELINE**
When a character is said to be "X years old in Arc 1," verify it makes sense with the timeline.

**Example:**
- Perlereina is ~35 in Arc 1
- The Duel was 18 years before Arc 1
- Therefore Perlereina was ~17 during the Duel ✓ (Master Lore confirms this)

**If math doesn't add up, FLAG IT to the user:**
"I notice Perlereina is listed as 35 in Arc 1, but the timeline says Kamigami were born 20 years ago. This creates a contradiction. Should I verify the timeline?"

---

### **RULE 5: WHEN IN DOUBT ABOUT PLOT EVENTS, CHECK CHARACTER ARCS**
Deaths, captures, revelations → these are in character profile "ARC-BY-ARC ROLE" sections.

```markdown
User: "When does Glayne die?"
Claude: [searches "Glayne death"]
Claude: [sees PERLEREINA_CHARACTER_PROFILE.md mentions "Glayne dies Arc 5"]
Claude: [calls view on GLAYNE_CHARACTER_PROFILE.md to verify]
Claude: "Glayne dies in Arc 5 (NOT Arc 1), during Perlereina's losses."
```

---

### **RULE 6: START EVERY SESSION BY READING THE QUICK_REF**
At the beginning of EVERY conversation about GID:
1. Call `view` on `GID_QUICK_REF_FINAL.md`
2. Read the entire file (it's short)
3. Use it as your baseline for fact-checking

**Why:** Prevents re-making the same errors across sessions.

---

### **RULE 7: NEVER ASSUME NARRATIVE CONVENTIONS**
Just because a character is "Arc 1 antagonist" doesn't mean they die in Arc 1.

```markdown
BAD ASSUMPTION:
"Glayne is Arc 1's villain, so he probably dies at the end of Arc 1."

CORRECT APPROACH:
"Let me check Glayne's profile to see when he dies."
[Finds: Dies Arc 5, is a recurring villain]
```

---

### **RULE 8: IF ASKED TO CREATE SUMMARIES, CITE SOURCES**
When creating documents like QUICK_REF, add a "VERIFICATION SOURCES" section:

```markdown
## VERIFICATION SOURCES
- Yonoa's age (33): YONOA_HOUZU_CHARACTER_PROFILE.md line 9
- Kamigami roster: GID_MASTER_LORE.md lines 101-104
- Glayne's death: PERLEREINA_CHARACTER_PROFILE.md line 565
```

**Why:** User can spot-check your work and trace errors back to source.

---

## WORKFLOW FOR ANSWERING USER QUESTIONS

### **SIMPLE QUESTIONS (Character age, faction, etc.):**
1. Search project knowledge for character name
2. View their character profile (lines 1-50 for basic info)
3. Answer with exact quote from file

### **COMPLEX QUESTIONS (Plot events, relationships):**
1. Search for relevant character profiles
2. View the "ARC-BY-ARC ROLE" or "RELATIONSHIPS" sections
3. Cross-reference with other involved characters
4. Answer with synthesis, citing which profiles

### **LORE QUESTIONS (Timeline, factions, power system):**
1. View GID_MASTER_LORE.md first
2. If more detail needed, view Factions.md or specific character profiles
3. Answer with citations

---

## RED FLAGS - STOP AND VERIFY IF YOU CATCH YOURSELF:

🚩 Writing "TBD" for something that might already exist
🚩 Saying "probably" or "likely" about plot events
🚩 Listing 4+ Kamigami (there are only 3)
🚩 Claiming someone dies in Arc 1 without checking
🚩 Inventing occupations (chocolatier, etc.)
🚩 Mixing up Free members and Pristania members
🚩 Stating ages without checking character profile headers

**When you see a red flag: STOP. Call view tool. Verify.**

---

## FOR THE USER: PASTE THIS INTO PROJECT INSTRUCTIONS

```markdown
# GID STORY DEVELOPMENT - CLAUDE'S RULES

## CRITICAL: VERIFICATION BEFORE CLAIMS
1. ALWAYS read character profiles before making claims about them
2. NEVER hallucinate occupations, relationships, or plot points
3. Use project_knowledge_search to FIND files, then use view to READ them
4. Start EVERY session by reading GID_QUICK_REF_FINAL.md
5. When uncertain, say "Let me verify that" and actually check

## THE FIVE PROTAGONISTS (Do NOT get this wrong)
1. Arjan (15) - Island, Gallan's ward
2. Lopney (15) - Island, Gallan's ward
3. Yonoa Houzu (33) - Jitsumoto heir
4. Ichiro Kiryuin (~17) - Free shopkeeper & stage magician
5. Lyzander Sugimori (~19) - Free, Meiji's son

## THE KAMIGAMI (Kami's THREE children - NOT four)
1. Diominiciel Dei (~40) - Eldest
2. Hirohiko Dei (~38) - Middle child
3. Perlereina Dei (~35) - Youngest

**Tairin is NOT a Kamigami. She is a Free member.**

## COMMON ERRORS TO AVOID
- ❌ Calling Cristopher a protagonist (he's supporting)
- ❌ Listing Tairin as a Kamigami (she's Free, not Kami's daughter)
- ❌ Saying Glayne dies in Arc 1 (he dies in Arc 5)
- ❌ Writing ages as "TBD" without checking profiles first
- ❌ Inventing occupations (always verify from profiles)

## VERIFICATION SOURCES
- Character basics: Individual character profile headers
- Timeline: GID_MASTER_LORE.md lines 95-250
- Kamigami roster: GID_MASTER_LORE.md lines 101-104
- Deaths/plot events: Character arc sections in profiles
- Quick facts: GID_QUICK_REF_FINAL.md

## WORKFLOW
1. User asks question
2. Claude searches project knowledge to find relevant file
3. Claude calls view on that file to verify
4. Claude answers with citation
5. If uncertain, Claude asks user to clarify rather than guessing
```

---

**END OF INSTRUCTIONS**
