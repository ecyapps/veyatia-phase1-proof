# 🚀 Quick Verification Commands

These are the exact commands to independently verify Veyatia Phase 1 is real and reproducible.

## One-Line Complete Verification

```bash
# Run all verification steps in sequence
./scripts/independent_verify.sh
```

## Step-by-Step Manual Verification

### 1. Fresh Environment Setup

```bash
# For completely fresh verification (optional)
cd /tmp
git clone --depth=1 https://github.com/ecyapps/veyatia-backend-0809-v1.git veyatia-verify
cd veyatia-verify

# OR work with existing clone
cd /path/to/veyatia-python-0808-v1
```

### 2. Set Deterministic Environment

```bash
# Critical for reproducibility
export PYTHONHASHSEED=0
export VEYATIA_SEED=42
export NUMPY_SEED=42
```

### 3. Core Guard Tests (Fast, High-Signal)

```bash
# Activate environment
source venv/bin/activate

# Test crown jewels (30 seconds)
python3 -m pytest -q tests/guards/test_crown_jewels_exist.py --maxfail=1 --disable-warnings

# Test immutable core (60 seconds) 
python3 -m pytest -q tests/core/test_immutable_core_break_tests.py --maxfail=1 --disable-warnings
```

**Expected output:**
```
....                                                 [100%]
4 passed in 0.56s

............                                         [100%]
12 passed in 2.40s
```

### 4. Evidence Collection Demo

```bash
# Run current proof (2 minutes)
./scripts/current_proof.sh
```

**Expected output:**
```
🔬 CURRENT PROOF: Evidence Collection Demo
==========================================

✅ ALL EVIDENCE COLLECTED

EVIDENCE ARTIFACTS:
• Environment fingerprint: artifacts/current_proof/.../environment.json
• API test evidence: artifacts/current_proof/.../api_test_evidence.json
• Proof summary: artifacts/current_proof/.../PROOF_SUMMARY.json
```

### 5. Tag and Commit Verification

```bash
# Check current commit
git rev-parse --short=7 HEAD

# Check for core tags
git tag -l | grep -i core
```

**Expected output:**
```
bbdbbc7  # (or another valid commit)
emotional-os-core-v1
stable-core-v1.5
```

### 6. CI-Style Verification

```bash
# Run with coverage (like CI does)
python3 -m pytest -q --cov=app --cov-branch tests/guards/test_crown_jewels_exist.py tests/core/test_immutable_core_break_tests.py
```

**Expected:** Tests pass (coverage may be lower than 35% with just these tests)

### 7. Full Forensic Proof (Optional)

```bash
# Complete evidence collection (5-10 minutes)
./scripts/final_proof_enhanced.sh

# Generate investor report
make report
```

## What Each Step Proves

| Step | Proves | Time |
|------|--------|------|
| Crown Jewels | Core implementations exist and work | 30s |
| Immutable Core | Zero regression, deterministic outputs | 60s |
| Evidence Collection | Forensic system functional | 2min |
| Tag Verification | Version locked and tagged | 5s |
| CI Verification | Local matches robot testing | 30s |
| Full Proof | Production-ready with audit trail | 10min |

## Green Light Criteria

✅ **Crown jewels test passes** (4/4 tests)  
✅ **Core break tests pass** (12/12 tests)  
✅ **Evidence artifacts created** with timestamps  
✅ **Core tags exist** (emotional-os-core-v1)  
✅ **API responds** (HTTP 200 with evidence)  
✅ **Test system works** (catches both passes and failures)

## If Something Fails

### Import Errors
```bash
# Make sure you're in project root
pwd  # Should end with veyatia-python-0808-v1
ls app/main.py  # Should exist

# Activate virtual environment
source venv/bin/activate
```

### Missing Dependencies
```bash
# Install core testing dependencies
pip install pytest pytest-cov
pip install fastapi pydantic
```

### Coverage Too Low
```bash
# See what's covered
python3 -m pytest --cov=app --cov-report=term-missing tests/guards/ tests/core/
```

### API Test Fails
```bash
# Check for port conflicts
lsof -i :8000
```

## Advanced Debugging

### View Evidence
```bash
# Browse latest evidence
ls -la artifacts/current_proof/$(ls -t artifacts/current_proof/ | head -1)/

# View API test evidence  
cat artifacts/current_proof/*/api_test_evidence.json | jq
```

### Run Individual Components
```bash
# Test just the archetype system
python3 -c "from app.services.signature.archetype_blender import ArchetypeCategory; print([c.name for c in ArchetypeCategory])"

# Test dual framing
python3 -c "from app.services.framing.dual_framing_engine import dual_framing_engine; print(dual_framing_engine.describe_emotion('joy', 'mystical'))"
```

### Check Environment Hash
```bash
# View environment fingerprint
cat artifacts/current_proof/*/environment.json | jq '.env_hash'
```

## Complete One-Command Verification

For ultimate simplicity:

```bash
# Single command that runs everything
source venv/bin/activate && export PYTHONHASHSEED=0 && ./scripts/independent_verify.sh
```

This command will:
1. Set deterministic environment
2. Run crown jewels tests
3. Run core break tests  
4. Generate evidence
5. Verify commit integrity
6. Run CI-style tests
7. Check file protection

**Result:** Complete verification with green/red output for each step.

---

**Bottom Line:** These commands provide independent verification that Veyatia Phase 1 is real, functional, and reproducible. No trust required—every step generates verifiable evidence.