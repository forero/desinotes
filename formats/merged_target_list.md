FROM TARGET DATABASE 
- Object-id   (int)
- RA  (float)
- DEC (float)
- Type (int64): Integer target mask. 

FROM STANDARDS FILE - (standard stars & sky positions) - not available - ideally some file on NERSC not SVN. Probably produced during target selection.
- Object-id (int)
- RA (float)
- DEC (float)
- Type (int64): Integer target mask. 


FROM TARGETSTRUCTURE FILE  
- ObservationalProgram (string): BRIGHT/DARK/ANY
- Type (int64): Integer target mask.
- Priority (int): These are the default priorities in absence of
spectroscopic knowledge. 
- ObservationsNeeded (int)


FROM DESIOBSERVATIONS DATABASE - not available
- Object-id (int)
- ObservedFlag (int)

FROM DESIRESULTS DATABASE - not available
- Object-id (int)
- Type (string)
- z_spec (float)

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
