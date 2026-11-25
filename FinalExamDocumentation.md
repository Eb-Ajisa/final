# First Looks

At FIRST LOOK THE QUALITY.YML FILE NEEDED FIXING
- Added PIT TEST
- Spot Bugs

It seems like all 14 Basic test given to us pass with no fail but the quality is definately trash. I got that from pulling the jacoco report

![alt text](image.png)

Over 740 methods missed, thats a lot over the span of:

146 Classes, 14 Test, 30% Coverage

[Initial PIT Run failed so running PIT in increments]

# Issues Found - Github Issues explains in more detail

- Improvement on test coverage
- Combat testing is lacking
- 47 Potnetial quality problems found by SPOTBUGS

Count Name                     
----- ----                     
   23 CT_CONSTRUCTOR_THROW     
   12 EI_EXPOSE_REP            
    6 EI_EXPOSE_REP2           
    3 MS_PKGPROTECT            
    1 ICAST_IDIV_CAST_TO_DOUBLE
    1 IM_BAD_CHECK_FOR_ODD     
    1 DCN_NULLPOINTER_EXCEPTION

# Inital Baseline and Risk Assesment Full v.

The initial assessment of *The Halls of 7800* revealed significant weaknesses in automated testing and potential software reliability risks.

Although all 14 existing JUnit tests passed, JaCoCo reported only **30% instruction coverage** and **20% branch coverage**. Much of the application's behavior therefore remains untested by the current suite.

PIT mutation testing of the combat package reported **20% mutation coverage** and **52% test strength**, suggesting limited test effectiveness. SpotBugs also identified **47 medium-priority warnings** requiring investigation.

### Risk Prioritization

| Risk | Supporting Evidence | Priority |
|---|---|---|
| Potential code-quality problems | 47 SpotBugs warnings | Medium |
| Untested UI and audio behavior | 0% automated instruction coverage in both packages | Medium |

These are preliminary risk ratings. Reported defects have not all been independently reproduced, and priorities may change after investigation.

### Beta-Reported Bugs

The five risks above correspond to these player reports in [BUGS.md](https://github.com/Eb-Ajisa/final/blob/main/BUGS.md):

| Reported bug | What the player reported |
|---|---|
| **Shield doesn't stop poison** | A poison bite applied poison even though shielding absorbed the entire hit. |
| **Lost my gold buying from Conover** | Buying armor with a full pack deducted gold and removed the armor from the shop, but did not give the player the item. |
| **Archivist only counts one requirements page** | Three torn requirements pages appeared as a stack, but the Archivist and quest log counted only one. |
| **"Continue" puts me somewhere else** | After saving, the player resumed in a different position with different health and a previously killed monster alive. The player mentioned an earlier snare, but its connection to the problem is unknown. |
| **Fell past a guardian** | A hidden trapdoor let the player descend from a guardian floor without defeating the guardian. |

These reports have not yet been confirmed or investigated. Individual GitHub Issues will be created during **Task 3**.

### Planned Quality Improvements

- [ ] Add targeted JUnit 5 tests for high-risk gameplay systems.
- [ ] Investigate and fix selected beta-reported defects.
- [ ] Improve instruction, branch, and mutation coverage.
- [ ] Investigate and resolve significant SpotBugs findings.
- [ ] Improve GitHub Actions continuous integration checks.
- [ ] Introduce at least one additional SQA tool or technique not previously required in the course.
- [ ] Verify improvements and compare final metrics against the initial baseline.

### Assessment Limitations

Passing tests do not guarantee that the game is defect-free. Likewise, SpotBugs warnings are potential problems rather than confirmed bugs.

The initial full-project PIT run encountered repeated worker timeouts. The recorded **20% mutation coverage applies only to the combat package** and must not be presented as the project's overall mutation score.

### Initial Conclusion

The Halls of 7800 successfully compiles and passes its existing automated tests, but the available testing evidence is insufficient to establish strong reliability. Improvements should prioritize core gameplay correctness, regression protection, test effectiveness, and maintainability.

Final measurements will be compared with this baseline to evaluate the impact of the changes.
  