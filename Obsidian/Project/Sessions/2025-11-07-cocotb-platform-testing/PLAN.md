# CocoTB Platform Testing Framework - Session Plan

**Session:** 2025-11-07-cocotb-platform-testing
**Branch:** sessions/2025-11-07-cocotb-platform-testing
**Status:** In Progress

## Mission
Upgrade @libs/forge-vhdl/ cocotb test infrastructure to create a MokuConfig-driven simulation platform that validates the FORGE control scheme (CR0[31:29] calling convention).

## Key Requirements
1. **Focus:** FORGE control scheme validation (NOT application-specific FSMs)
2. **Location:** libs/forge-vhdl/cocotb_test/platform/ (natural extension)
3. **Network CR API:** Explicit primitives with ~200ms delays
4. **Target Configs:** Support bpd-deployment-setup1-dummy-dut.yaml and setup2-real-dut.yaml
5. **Features:** Multi-channel capture, routing simulation, trigger modes

## Phase 1: Foundation (Week 1) ✅ IN PROGRESS

### Completed
- [x] Directory structure created
- [x] Backend abstraction (backend.py)
- [x] Network CR primitives with delays (network_cr.py)
- [x] Oscilloscope simulator (oscilloscope.py)
- [x] CloudCompile passthrough (cloud_compile.py)
- [x] Simulation backend (simulation_backend.py)

### Remaining
- [x] FORGE control validation tests ✅ (test_platform_forge_control.py - 208 lines, 2 test cases)
- [ ] Simple counter PoC with FORGE scheme
- [ ] Integration test with deployment YAMLs
- [ ] Quick-start documentation

### Key Files Created
```
libs/forge-vhdl/cocotb_test/platform/
├── __init__.py
├── backend.py                    # Abstract Backend interface
├── network_cr.py                 # Network CR with 200ms delays
├── simulation_backend.py         # MokuConfig-driven coordinator
└── simulators/
    ├── __init__.py
    ├── oscilloscope.py          # Behavioral oscilloscope
    └── cloud_compile.py         # CloudCompile passthrough
```

### Implementation Details
- **test_platform_forge_control.py**: 2 test cases validating CR0[31:29] sequencing
  - `test_forge_control_sequence()`: Tests power-on state, enable sequence, network delays
  - `test_network_cr_primitives()`: Tests concurrent CR updates, network statistics
- **Network delays**: Successfully implemented 200ms realistic delays
- **Commit history**: 2 commits (2435389, 8cbf9ff) with 1,590 lines added

## Phase 2: BPD Deployment Validation (Week 2)

### Goals
- Load and test bpd-deployment-setup1-dummy-dut.yaml
- Load and test bpd-deployment-setup2-real-dut.yaml
- Validate 2-slot routing (Slot2OutD → Slot1InA for debug bus)
- Test network CR updates with BPD registers

### Deliverables
- [ ] test_platform_bpd_deployment.py
- [ ] Routing matrix validation
- [ ] CR update sequence tests
- [ ] Debug bus capture validation

## Phase 3: Advanced Features (Week 3)

### Goals
- Complete routing matrix (IN/OUT/Slot connections)
- Oscilloscope trigger modes
- Multi-channel simultaneous capture
- Cross-platform testing (Go/Lab/Pro)

### Deliverables
- [ ] Enhanced routing simulation
- [ ] Trigger mode support
- [ ] Platform matrix tests
- [ ] Performance benchmarks

## Phase 4: Agent Architecture Review

### Decision Point
After Phase 2, evaluate if specialized agent needed:

**Option A: No Agent** ✅ RECOMMENDED
- Standard Python/CocoTB development
- Use existing run.py infrastructure

**Option B: Light Generation Agent** (Future)
- Auto-generate tests from YAML configs
- Only if patterns emerge

## Web UI Coordination Opportunities

### Parallel Work (Phase 1)
**Web UI Team:**
- MokuConfig YAML editor
- Network CR control panel
- Deployment dashboard

**CLI Team:**
- Platform infrastructure (this work)
- FORGE validation tests

### Integration Points (Phase 2)
- Web UI → Network CR updates → Simulator
- Simulator → Oscilloscope data → Web UI
- Test results → Dashboard display

## Quick-Start Commands

```bash
# Setup
cd libs/forge-vhdl
mkdir -p cocotb_test/platform/simulators
mkdir -p cocotb_test/platform_tests
mkdir -p cocotb_test/test_duts

# Run FORGE control test (once created)
uv run python cocotb_test/run.py platform_forge_control

# Run with deployment YAML
uv run python cocotb_test/run.py platform_bpd_deployment \
  --config ../../bpd-deployment-setup1-dummy-dut.yaml
```

## Success Metrics

### Phase 1 ✅
- [x] Network CR API with 200ms delays
- [x] MokuConfig drives simulator setup
- [x] Oscilloscope captures signals
- [x] FORGE control scheme validated ✅

### Phase 2
- [ ] Both deployment YAMLs work
- [ ] Routing matrix functional
- [ ] Debug bus visible

### Phase 3
- [ ] Multi-channel capture
- [ ] Trigger modes work
- [ ] Cross-platform validated

## Key Innovation
Network-settable CR primitives with realistic delays create explicit boundary between "outside world" (Python scripts) and FPGA simulation, matching real MCC behavior.

## Current Status
Phase 1 infrastructure and FORGE validation complete (70%). Need to:
1. ~~Create FORGE validation tests~~ ✅ DONE
2. Build simple counter PoC
3. Test with deployment YAMLs
4. Document quick-start

## Next Actions
1. ~~Create test_platform_forge_control.py~~ ✅ DONE (commit 8cbf9ff)
2. Create forge_counter.vhd test DUT
3. ~~Validate FORGE control sequencing~~ ✅ DONE
4. ~~Test network CR delays~~ ✅ DONE (200ms delays verified)

## Time Estimate
- Phase 1: 3-4 days (70% complete - FORGE tests done, need counter PoC + docs)
- Phase 2: 3-4 days
- Phase 3: 4-5 days
- **MVP Total:** 1-2 weeks for Phase 1+2

## Notes
- Focus on FORGE control scheme, not BPD-specific FSM
- Network delays critical for realistic simulation
- Routing simulation sufficient for 2-slot setups
- Agent creation deferred until patterns emerge