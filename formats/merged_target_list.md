FROM TARGET DATABASE 
- Object-id   (int)
- RA  (float)
- DEC (float)
- ApparentType (string)
- * Type (int64): Integer target mask. Tackles the issue of targets
belonging to more than one class. [How often does that happen?]* 

FROM STANDARDS FILE - (standard stars & sky positions) - not available
- Object-id (int)
- RA (float)
- DEC (float)
- ApparentType (string)
- * Type (int64): Integer target mask. Standard star might overlap
with bright time targets [How often does that happen?]* 

FROM DESIRESULTS DATABASE - not available
- Object-id (int)
- DesiType (string)
- ObservationsDone (int)
- z_spec (float)
- **

FROM TARGETSTRUCTURE FILE - not available
- Type (string)
- ObservationsNeeded (int)
- ObservationalProgram (string): BRIGHT/DARK
- Priority (int): These are the default priorities in absence of
spectroscopic knowledge. *We might want different priorities for
different LRGs*

FROM TILING FILE
- Layer (int): Right now each tileid belongs to a different
layer. Priorities might change for the last year/layer.

WRITE MERGEDTARGETLIST FILE (INPUT TO FIBERASSIGN)
- Object-id (int)
- RA (float)
- DEC (float)
- FiberPriority (int)
- FiberObservationsNeeded (int)


Other comments
==============

* (Stephen) There may be additional information (similar to the object-id) that
we probably want to pass through for convenience, even if they aren't
used by the fiber assignment algorithm itself.  The documentation
should be clear about "these are needed for the algorithm" and "these
are passed through from input to output for convenience".  e.g. the
target selection bitmask (i.e. the object type(s)) — pass them forward
for convenience, but the FiberPriority and FiberObservationsNeeded are
what are actually used by the fiber assignment algorithm. 
 
* (Stephen) One missing piece is how to specify the possibility of an
  ancillary program with "observe N objects from this list of M>>N
  targets".  I'm not sure how to easily do that. 

* (Stephen) When I comes time to define actual file formats and
  database tables, I'll have opinions about CamelCaps vs. under_scores
  and exact variable names. 
