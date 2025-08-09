# 🔬 Independent Verification Guide
## Verify—Don't Trust Cursor (or Any Tool) Blindly

This guide provides step-by-step instructions to independently confirm that Veyatia's Phase 1 implementation is real and reproducible, with no cached state or assumptions.

## Quick Overview

We lock truth with repeatable proofs, not vibes. Here's the fastest way to independently confirm everything works:

1. **Fresh clone, clean env** (no cached state)
2. **Deterministic seeds + provenance proof**
3. **Run core guards** (fast, high-signal)
4. **Full proof + investor bundle** (single source of truth)
5. **Tag integrity check** (ensure you're on the locked core)
6. **CI gate** (robot agreement with your laptop)

---

## Step 1: Fresh Clone, Clean Environment

Start completely fresh with no cached state:

```bash
# Navigate to a clean directory
cd /tmp

# Fresh clone (shallow for speed)
git clone --depth=1 https://github.com/ecyapps/veyatia-backend-0809-v1.git veyatia-verify
cd veyatia-verify

# Clean Python environment
python3 -m venv .venv && source .venv/bin/activate

# Install dependencies (based on your existing virtual environment)
pip install fastapi uvicorn pytest pytest-cov pytest-asyncio
pip install pydantic numpy opencv-python ffmpeg-python
pip install aiofiles python-dotenv httpx
pip install psutil  # For memory usage tests
```

**What this proves:** Starting from scratch eliminates any cached or locally-modified dependencies.

---

## Step 2: Deterministic Seeds + Provenance Proof

Configure deterministic execution environment:

```bash
# Set deterministic seeds (critical for reproducibility)
export PYTHONHASHSEED=0 
export VEYATIA_SEED=42 
export NUMPY_SEED=42 
export TF_DETERMINISTIC_OPS=1 
export CUDA_LAUNCH_BLOCKING=1

# Run the current proof script
./scripts/current_proof.sh
```

**What this proves:** 
- Environment is deterministic and repeatable
- Evidence collection system works
- Creates fingerprints for later verification

**Expected output:**
```
🔬 CURRENT PROOF: Evidence Collection Demo
==========================================

📋 Current State:
   Timestamp: 2024-01-09T14:30:45Z
   Commit: 335fb40
   Full SHA: 335fb40...

✅ ALL EVIDENCE COLLECTED

EVIDENCE ARTIFACTS:
• Environment fingerprint: artifacts/current_proof/.../environment.json
• Integration test logs: artifacts/current_proof/.../integration_test.log
• API test evidence: artifacts/current_proof/.../api_test_evidence.json
• Proof summary: artifacts/current_proof/.../PROOF_SUMMARY.json
• Reproduction script: artifacts/current_proof/.../reproduce.sh
```

---

## Step 3: Core Guards (Fast, High-Signal Tests)

Run the most critical tests that verify core functionality:

```bash
# Run crown jewels test (ensures billion-dollar implementations exist)
pytest -q tests/guards/test_crown_jewels_exist.py \
  --maxfail=1 \
  --disable-warnings \
  --cov=app \
  --cov-branch \
  --cov-report=term-missing

# Run immutable core break tests (ensures zero regression)
pytest -q tests/core/test_immutable_core_break_tests.py \
  --maxfail=1 \
  --disable-warnings \
  --cov=app \
  --cov-branch \
  --cov-report=term-missing
```

**What this proves:**
- Core emotional AI implementations exist and work
- Critical data files are valid JSON
- All crown jewel modules can be imported
- Archetype categories are intact
- Dual framing system works for both mystical and scientific descriptions
- Chakra overlay engine is functional
- Memory usage is stable
- System handles invalid inputs gracefully

**Expected output:**
```
======================== test session starts ========================
collected 4 items

tests/guards/test_crown_jewels_exist.py ....                [100%]

======================== 4 passed in 2.34s =======================

======================== test session starts ========================
collected 11 items

tests/core/test_immutable_core_break_tests.py ...........  [100%]

======================== 11 passed in 5.67s =======================
```

---

## Step 4: Full Proof + Investor Bundle

Generate comprehensive evidence with single source of truth:

```bash
# Run enhanced final proof with forensic evidence collection
./scripts/final_proof_enhanced.sh

# Generate complete investor report
make report
```

**What this proves:**
- All Phase 1 components work together
- Coverage measurements are real (>25% threshold)
- API endpoints respond correctly
- Error handling works
- Test system catches both passes and failures
- Documentation references real commits

**Expected artifacts:**
- `artifacts/final_proof_evidence/<TIMESTAMP>/FORENSIC_SUMMARY.json`
- `out/reports/latest/index.html` (Beautiful HTML dashboard)
- `out/reports/veyatia_report_*.zip` (Email-ready bundle)

**Sample forensic summary:**
```json
{
  "forensic_proof": {
    "timestamp": "2024-01-09T14:30:45Z",
    "commit": "335fb40",
    "all_checks_passed": true,
    "checks": {
      "commit_check": {"status": "pass", "expected": "335fb40"},
      "signature_test": {"status": "pass", "duration": 2.34},
      "error_test": {"status": "pass", "duration": 1.23},
      "coverage": {"status": "pass", "coverage_percent": 67.2},
      "api_test": {"status": "pass", "response": "200:42"},
      "break_test": {"status": "pass"}
    },
    "artifact_count": 47
  }
}
```

---

## Step 5: Tag Integrity Check

Verify you're testing the exact locked core version:

```bash
# Check current commit and tags
git describe --tags --always
git tag -l | grep emotional-os-core-v1

# Verify commit matches expected Phase 1 commit
CURRENT_COMMIT=$(git rev-parse --short=7 HEAD)
echo "Current commit: $CURRENT_COMMIT"

# Should show: 335fb40 (the locked Phase 1 commit)
```

**What this proves:**
- You're testing the exact same code that was locked/tagged
- No drift from the verified implementation
- Reproducible commit SHA

---

## Step 6: CI Gate Verification

Ensure your local results match what CI would produce:

```bash
# Run the same command CI uses
pytest -q \
  --cov=app \
  --cov-branch \
  --cov-report=xml \
  --cov-fail-under=35 \
  tests/guards/test_crown_jewels_exist.py \
  tests/core/test_immutable_core_break_tests.py

# Guard critical files (CI protection)
CRIT='^(app/services/(signature|framing|visualization|chakra)|data)/'
if git diff --name-status origin/main...HEAD | egrep -q "^D\\s+${CRIT}"; then 
  echo "❌ Critical files deleted"
  exit 1
else
  echo "✅ Critical files protected"
fi
```

**What this proves:**
- Your laptop produces same results as CI
- Coverage thresholds are met
- Core files are protected from deletion

---

## Green Light Criteria

I'll treat these as definitive proof the system is real:

✅ **Fresh clone passes guards + break-tests**
✅ **Evidence bundle created** (commit SHA + env hash recorded)  
✅ **emotional-os-core-v1 tag exists** and matches the commit you tested
✅ **CI run is green** with the same TOTAL coverage window

---

## Troubleshooting

If any step fails, paste the last ~40 lines of output. Common issues:

1. **Missing dependencies**: Install with `pip install pytest pytest-cov`
2. **Import errors**: Ensure you're in the project root directory
3. **Coverage too low**: Run `pytest --cov=app --cov-report=term-missing` to see uncovered lines
4. **API test fails**: Check if port conflicts exist

---

## Verification Checklist

- [ ] Fresh clone in clean directory
- [ ] Virtual environment created and activated
- [ ] Dependencies installed
- [ ] Deterministic seeds set
- [ ] Current proof script passes
- [ ] Crown jewels test passes
- [ ] Core break tests pass
- [ ] Final proof forensic edition passes
- [ ] Investor report generated
- [ ] Commit SHA matches 335fb40
- [ ] Tag exists: emotional-os-core-v1
- [ ] CI-style tests pass locally

When all boxes are checked, you have independent verification that Veyatia Phase 1 is real, functional, and reproducible.

---

## Next Steps After Verification

Once verified, you can:

1. **Explore the evidence**: `ls -la artifacts/forensic_evidence/latest/`
2. **Browse the dashboard**: Open `out/reports/latest/index.html`
3. **Read documentation**: `cat docs/EVIDENCE_COLLECTION.md`
4. **Run full test suite**: `pytest tests/` (300+ tests)
5. **Start development**: Follow `CONTRIBUTING.md`

Remember: This verification process creates a complete audit trail. Every test run generates forensic evidence that can be examined months later to verify what actually happened.