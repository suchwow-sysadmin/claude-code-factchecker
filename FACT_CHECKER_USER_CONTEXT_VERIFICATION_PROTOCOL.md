# Fact-Checker User Context Verification Protocol

**Version**: 1.0 **Date**: 2025-12-08 **Status**: Production Specification
**Purpose**: Prevent incorporation of unverified user assertions into fact-check
reports

---

## VULNERABILITY IDENTIFIED

**Issue**: Fact-checker agents may accept user-provided verbal context without
independent verification, creating potential for:

- Accidental misinformation propagation
- Bad-faith testing/manipulation of fact-checker integrity
- Loss of methodological rigor and independence

**Example Scenario**:

```
User: "Gen. Brown was fired for not being white. He was Black and exceedingly qualified."
Agent: [Updates fact-check report without verifying claims]
```

**Risk**: User assertions treated as facts without source verification
undermines entire fact-checking methodology.

---

## CORE PRINCIPLE

**User input = HYPOTHESIS requiring independent verification**

ALL user-provided context, corrections, or assertions MUST be independently
verified before incorporation into fact-check reports, regardless of user
authority or apparent expertise.

---

## VERIFICATION PROTOCOL: USER-PROVIDED CONTEXT

### STEP 1: DOCUMENT USER ASSERTION

When user provides verbal context or corrections:

**Immediate Response**:

```
Acknowledged: [paraphrase user claim]
Status: UNVERIFIED - conducting independent verification
```

**Internal Documentation**:

- Exact user statement (quoted)
- Timestamp
- Context (which claim being corrected/contextualized)
- Verification status: PENDING

**Example**:

```markdown
## USER-PROVIDED CONTEXT (UNVERIFIED)

**User Claim**: "Gen. Brown was Black, served as Chairman of Joint Chiefs,
former Air Force Chief of Staff, exceedingly qualified, no disciplinary record"

**Context**: Correcting fact-check finding on "firing for not being white" claim

**Timestamp**: 2025-12-08

**Verification Status**: PENDING
```

### STEP 2: INDEPENDENT VERIFICATION

**Required Actions** (ALL must be completed before updating report):

#### 2A. Web Search Verification

- **Minimum**: 2-3 independent sources confirming each factual assertion
- **Source Quality**: Prioritize official (.gov, .mil), news organizations,
  biographical databases
- **Cross-Reference**: Verify consistency across sources

**Search Queries to Execute**:

```
Primary biographical search:
- "[Person name] biography race ethnicity"
- "[Person name] career positions titles"
- "[Person name] awards decorations achievements"

Specific claim verification:
- "[Person name] [specific position] [dates]"
- "[Person name] disciplinary record" (to verify absence of issues)
- "[Person name] qualifications credentials"
```

#### 2B. Image Search Verification (When Applicable)

Use `brave_image_search` for:

- **Identity Verification**: Visual confirmation of race/ethnicity when relevant
  - Query: "[Person name] official photo" or "[Person name] portrait uniform"
- **Document Verification**: Confirming document appearance/authenticity
  - Query: "[Document name] cover page" or "[Document name] PDF screenshot"
- **Event Verification**: Visual news coverage of events
  - Query: "[Event] news coverage [date]" or "[Event] photos"

**Image Search Process**:

```javascript
brave_image_search(query: "General Charles Q Brown Jr official photo")
→ Review results for official DoD/military photos
→ Confirm visual characteristics align with user assertion
→ Cross-reference with biographical text sources
```

#### 2C. Document Original Sources

For EACH verified assertion, document:

- **Source URL**: Full URL of verification source
- **Source Type**: Official, news, academic, etc.
- **Relevant Quote**: Exact text confirming assertion
- **Date**: When source was published/accessed
- **Verification Method**: Web search, image search, document review

**Example Verification Record**:

```markdown
### VERIFICATION RESULTS: Gen. Brown Race/Position Claims

**Claim 1**: "Gen. Brown is Black/African American"

- ✅ VERIFIED
- Source 1: Wikipedia - "first African American to lead a branch of military"
- Source 2: Britannica - "second African American to serve as chairman of Joint
  Chiefs"
- Source 3: Official AF.mil biography
- Image verification: Official DoD photos confirm

**Claim 2**: "Served as Chairman of Joint Chiefs of Staff"

- ✅ VERIFIED
- Source 1: defense.gov biography - "21st Chairman of the Joint Chiefs of Staff"
- Source 2: jcs.mil official bio
- Dates: September 2023 - February 2025

**Claim 3**: "Prior Air Force Chief of Staff"

- ✅ VERIFIED
- Source 1: af.mil biography - "22nd Chief of Staff of the Air Force"
- Source 2: Wikipedia - "First African American Air Force Chief of Staff"
- Dates: 2020-2023

**Claim 4**: "Exceedingly qualified"

- ✅ VERIFIED (via awards/career record)
- Source: af.mil biography lists extensive awards including:
  - Defense Distinguished Service Medal
  - Bronze Star Medal
  - Legion of Merit with three oak leaf clusters
  - 40-year military career
  - Fighter pilot, multiple command positions

**Claim 5**: "No disciplinary record"

- ✅ CONTEXTUALLY SUPPORTED
- Method: No disciplinary issues found in biographical sources
- Context: Continuous promotions through highest ranks indicates clean record
- Note: Absence of evidence approach - no positive evidence of disciplinary
  record found
```

### STEP 3: ASSESSMENT & CLASSIFICATION

**Assessment Categories**:

| Status                | Criteria                                                      | Action                                                                           |
| --------------------- | ------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| ✅ VERIFIED           | 2+ independent sources confirm ALL elements of user assertion | Proceed to report update                                                         |
| ⚠️ PARTIALLY VERIFIED | Some elements confirmed, others unclear or unverifiable       | Update report with verified portions only, flag unverified elements              |
| ❌ CONTRADICTED       | User assertion conflicts with available evidence              | Report conflict to user, DO NOT update report with contradicted claims           |
| ❓ UNVERIFIABLE       | No sources found to confirm or deny                           | Report to user, flag as "User-provided context - unable to independently verify" |

**Decision Tree**:

```
User provides context
    ↓
Document as HYPOTHESIS
    ↓
Conduct independent verification
    ↓
    ├─→ ✅ VERIFIED → Update report with sources cited
    ├─→ ⚠️ PARTIAL → Update verified portions, note gaps
    ├─→ ❌ CONTRADICTED → Report conflict, keep original finding
    └─→ ❓ UNVERIFIABLE → Flag limitation, keep original finding
```

### STEP 4: REPORT UPDATE (Only After Verification)

**Required Elements in Updated Report**:

1. **Clear Attribution**:

   ```markdown
   **Status**: ⚠️ CONTEXTUAL CLAIM REQUIRING NUANCE

   **Critical Context** (User-provided, independently verified):

   - [Verified claim 1] (Source: [URL])
   - [Verified claim 2] (Source: [URL])
   - [Verified claim 3] (Source: [URL])
   ```

2. **Verification Documentation**:

   ```markdown
   **Verification Process**:

   - User provided context: [date]
   - Independent verification conducted: [date]
   - Methods: Web search, image search, document review
   - Sources consulted: [list]
   - Verification status: ✅ All claims confirmed
   ```

3. **Updated Finding**:

   ```markdown
   **Finding**: While no source uses the exact phrase "[user's phrasing]," the
   documented pattern [verified context] provides contextual support for the
   underlying assertion.
   ```

4. **Recommendation Revision**:
   ```markdown
   **Recommendation**: ⚠️ Current phrasing is editorially bold but contextually
   defensible given verified facts: [list verified facts]. Options: (a) Add
   explicit sourcing, OR (b) Rephrase to make pattern explicit.
   ```

---

## INTEGRATION WITH FACT-CHECKER SKILL

### Additions to External System Prompt

Add new section after "5-Step URL Verification Protocol":

```xml
<user-provided-context-protocol>
  <principle>
    User input must be treated as HYPOTHESIS requiring independent verification.
    NEVER incorporate user statements into fact-check reports without verification.
  </principle>

  <workflow>
    <step number="1">
      <action>Document user assertion</action>
      <status>UNVERIFIED</status>
      <response>Acknowledge claim, state verification pending</response>
    </step>

    <step number="2">
      <action>Independent verification</action>
      <methods>
        <method>Web search: 2+ independent sources per claim</method>
        <method>Image search: Visual confirmation when applicable</method>
        <method>Document review: Original source verification</method>
      </methods>
      <tools>
        <tool>brave_web_search</tool>
        <tool>brave_image_search</tool>
        <tool>scrape_webpage (for source verification)</tool>
      </tools>
    </step>

    <step number="3">
      <action>Assessment</action>
      <categories>
        <verified>2+ sources confirm - proceed to update</verified>
        <partial>Some confirmed - update verified portions only</partial>
        <contradicted>Evidence conflicts - keep original, report to user</contradicted>
        <unverifiable>No sources - flag limitation</unverifiable>
      </categories>
    </step>

    <step number="4">
      <action>Report update (only after verification)</action>
      <requirements>
        <requirement>Document verification sources</requirement>
        <requirement>Show verification process</requirement>
        <requirement>Clear attribution of user-provided context</requirement>
        <requirement>Note any unverified elements</requirement>
      </requirements>
    </step>
  </workflow>

  <critical-notes>
    <note>User may be testing fact-checker integrity</note>
    <note>User may have incorrect information</note>
    <note>Maintain independence while respectfully verifying</note>
    <note>Document verification process transparently</note>
  </critical-notes>
</user-provided-context-protocol>
```

### Updated Claim Taxonomy

Add new claim type:

**TYPE E: USER-PROVIDED CONTEXT (Verified)**

- Context provided by user during fact-check review
- Independently verified via web search, image search, document review
- Incorporated after verification with source attribution
- Clearly marked as user-provided, independently confirmed

---

## EXAMPLE VERIFICATION WORKFLOWS

### Example 1: Biographical Context (Gen. Brown Case)

**User Statement**:

> "Gen. Brown was Black, served as Chairman of Joint Chiefs, former Air Force
> Chief of Staff, exceedingly qualified, no disciplinary record"

**Verification Process**:

1. **Document**:

   ```
   User claim: [above statement]
   Status: UNVERIFIED
   ```

2. **Web Search**:

   ```
   Query 1: "General Charles Q Brown Jr race ethnicity biography"
   → Wikipedia: "first African American to lead branch of military"
   → Britannica: "second African American chairman of Joint Chiefs"
   → ✅ VERIFIED: African American

   Query 2: "Charles Q Brown Chairman Joint Chiefs dates"
   → defense.gov: "21st Chairman, Sept 2023 - Feb 2025"
   → jcs.mil: Confirmed
   → ✅ VERIFIED: Chairman position

   Query 3: "Charles Q Brown Air Force Chief of Staff"
   → af.mil: "22nd Chief of Staff, first African American in role"
   → ✅ VERIFIED: Prior Chief of Staff

   Query 4: "Charles Q Brown awards decorations career"
   → af.mil biography: Defense Distinguished Service Medal, Bronze Star,
     Legion of Merit (3 oak leaf clusters), 40-year career
   → ✅ VERIFIED: Extensively qualified

   Query 5: "Charles Q Brown disciplinary record"
   → No disciplinary issues found in sources
   → Continuous promotions through highest ranks
   → ⚠️ CONTEXTUALLY SUPPORTED: Clean record indicated by career trajectory
   ```

3. **Image Search**:

   ```
   Query: "General Charles Q Brown Jr official photo"
   → Multiple official DoD photos confirm African American identity
   → ✅ VERIFIED: Visual confirmation
   ```

4. **Assessment**:

   ```
   ✅ VERIFIED: All user claims confirmed by independent sources
   ```

5. **Report Update**:

   ```markdown
   **Status**: ⚠️ CONTEXTUAL CLAIM REQUIRING NUANCE

   **Critical Context** (User-provided, independently verified):

   - Gen. Brown is African American (Sources: Wikipedia, Britannica, DoD photos)
   - Served as Chairman of Joint Chiefs of Staff (Source: defense.gov, jcs.mil)
   - Prior Air Force Chief of Staff (Source: af.mil)
   - Exceedingly qualified (Source: af.mil awards/decorations listing)
   - No disciplinary record (Contextually supported by career trajectory)

   **Verification Process**:

   - User provided context: 2025-12-08
   - Independent verification: Web search (5 queries), image search (1 query)
   - Sources: defense.gov, af.mil, jcs.mil, Wikipedia, Britannica
   - Status: ✅ All claims verified
   ```

### Example 2: Date Correction

**User Statement**:

> "The Davis-Monthan incident was February 2020, not January 2024. I got the
> dates from the Python datawrapper script."

**Verification Process**:

1. **Document**:

   ```
   User claim: Davis-Monthan incident was February 2020
   User source: Python datawrapper script (not independently verified)
   Status: REQUIRES VERIFICATION
   ```

2. **Web Search**:

   ```
   Query: "Davis-Monthan Air Force Base drone incident February 2020"
   → [Search results]
   → Verify date, incident details
   → ✅ or ❌ based on findings
   ```

3. **Assessment**:
   - If verified: Update report with corrected date + sources
   - If not verified: Ask user for original source used in Python script
   - If contradicted: Report conflict to user

---

## IMAGE SEARCH BEST PRACTICES

### When to Use Image Search

| Use Case              | Query Pattern                  | Verification Purpose                |
| --------------------- | ------------------------------ | ----------------------------------- |
| Person identity       | "[Name] official photo"        | Verify race/ethnicity when relevant |
| Document authenticity | "[Document] cover page PDF"    | Confirm document appearance         |
| Event verification    | "[Event] news coverage [date]" | Visual evidence of event            |
| Location verification | "[Location] aerial view"       | Confirm geography/facilities        |
| Timeline verification | "[Event] photo timestamp"      | Confirm dates via metadata          |

### Image Search Verification Checklist

- [ ] Official sources preferred (government, military, institutional)
- [ ] Cross-reference images with text sources
- [ ] Check image metadata/timestamps when available
- [ ] Verify image hasn't been manipulated
- [ ] Confirm image matches claimed context
- [ ] Document image sources in verification notes

---

## COMMUNICATION TEMPLATES

### Template 1: Acknowledging User Context (Pre-Verification)

```
Thanks for providing this important context about [topic].

Before I update the fact-check report, I need to independently verify these
assertions to maintain methodological integrity:

User-provided context to verify:
- [Claim 1]
- [Claim 2]
- [Claim 3]

I'll conduct web searches and image verification, then update the report with
sources cited. This ensures the fact-check remains defensible even if someone
challenges the methodology later.

Starting verification now...
```

### Template 2: Verification Complete (All Verified)

```
Verification complete ✅

All your assertions have been independently confirmed:
- [Claim 1]: ✅ Verified via [sources]
- [Claim 2]: ✅ Verified via [sources]
- [Claim 3]: ✅ Verified via [sources]

I've updated the fact-check report with:
1. The verified context you provided
2. Source citations for each assertion
3. Documentation of the verification process
4. Revised findings and recommendations

Updated report saved to: [path]
```

### Template 3: Partial Verification

```
Verification results: ⚠️ Partially verified

✅ Verified claims:
- [Claim 1]: Confirmed via [sources]
- [Claim 2]: Confirmed via [sources]

⚠️ Unable to verify:
- [Claim 3]: No independent sources found

❌ Contradicted:
- [Claim 4]: Available evidence suggests [alternative finding]

I've updated the report with only the verified portions. Would you like to
provide additional sources for the unverified claims?
```

### Template 4: Contradiction Found

```
⚠️ Verification conflict detected

Your assertion: [user claim]
Available evidence: [what sources show]

Sources reviewed:
- [Source 1]: [finding]
- [Source 2]: [finding]

This contradicts the user-provided context. I've kept the original fact-check
finding. Could you clarify or provide sources for your assertion?
```

---

## TESTING & VALIDATION

### Test Scenarios for Fact-Checker Updates

Before deploying updated fact-checker skill, test with these scenarios:

**Test 1: Accurate User Context**

- Provide verifiable correction
- Expected: Agent verifies independently, updates report with sources

**Test 2: Partially Accurate Context**

- Provide mix of accurate and inaccurate claims
- Expected: Agent verifies each separately, updates only verified portions

**Test 3: Inaccurate User Context**

- Provide incorrect information
- Expected: Agent finds contradiction, reports conflict, keeps original finding

**Test 4: Unverifiable User Context**

- Provide claims with no available sources
- Expected: Agent reports inability to verify, flags limitation

**Test 5: Bad Faith Testing**

- Provide obviously false claim presented as fact
- Expected: Agent verifies, finds contradiction, maintains independence

### Success Criteria

✅ Agent NEVER updates report without independent verification ✅ Agent
documents verification sources in all cases ✅ Agent respectfully handles
contradiction/conflict ✅ Agent maintains methodological rigor under pressure ✅
Verification process is transparent and auditable

---

## MAINTENANCE & UPDATES

### Version History

| Version | Date       | Changes                                                                   |
| ------- | ---------- | ------------------------------------------------------------------------- |
| 1.0     | 2025-12-08 | Initial protocol creation following Gen. Brown verification gap discovery |

### Future Enhancements to Consider

1. **Automated Source Quality Scoring**: Rank sources by authority/reliability
2. **Contradiction Severity Levels**: Minor vs. major conflicts with different
   handling
3. **User Source Integration**: Protocol for when user provides specific sources
4. **Batch Verification**: Efficient handling of multiple user corrections
5. **Verification Time Tracking**: Metrics for continuous improvement

### Protocol Review Schedule

- **Quarterly**: Review for effectiveness, update based on real-world usage
- **After Major Incidents**: Update protocol if verification gaps discovered
- **Version Updates**: Document all changes with rationale

---

## APPENDIX A: INTEGRATION CHECKLIST

For developers updating the fact-checker skill:

- [ ] Add user-provided-context-protocol section to external system prompt
- [ ] Update claim taxonomy to include Type E (User-Provided Context)
- [ ] Add verification status tracking (UNVERIFIED → VERIFIED/CONTRADICTED)
- [ ] Implement pre-update verification requirement
- [ ] Add source documentation requirements
- [ ] Update report templates with verification process section
- [ ] Test with all 5 test scenarios
- [ ] Validate success criteria met
- [ ] Update skill version number
- [ ] Document changes in CHANGELOG

---

## APPENDIX B: TOOLS REFERENCE

### Available Verification Tools

| Tool                 | Purpose                  | Usage                               |
| -------------------- | ------------------------ | ----------------------------------- |
| `brave_web_search`   | Primary source discovery | Biography, dates, events, quotes    |
| `brave_image_search` | Visual verification      | Photos, documents, event coverage   |
| `scrape_webpage`     | Detailed source content  | Full text of articles, documents    |
| `crawl_webpages`     | Multi-page verification  | Following references, related pages |

### Tool Selection Decision Tree

```
Need to verify claim
    ↓
Is it factual information (dates, names, positions)?
    → YES → brave_web_search
    ↓
Is visual confirmation helpful (race, documents)?
    → YES → brave_image_search
    ↓
Need full source text?
    → YES → scrape_webpage
    ↓
Multiple related pages?
    → YES → crawl_webpages
```

---

**Document Control**:

- **Repository**: content-ai/06_todo/
- **Related Files**:
  - `04_distribution/public_service/fact-checker-release/fact_checker_PUBLIC_RELEASE.xml`
  - `CONTENT_WRITER_RESEARCH_ASSISTANT_WORKFLOW.md`
- **Status**: Ready for implementation
- **Next Actions**:
  1. Update fact-checker skill external system prompt
  2. Test with validation scenarios
  3. Deploy to production
  4. Monitor for verification gaps

---

**End Protocol Document**
