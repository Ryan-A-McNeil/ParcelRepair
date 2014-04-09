ParcelRepair
============

Transforms a City of Detroit parcel number (or its constituent ward and item numbers) into the format prescribed by the assessment units in Detroit and Wayne County.


Mask Format
-----------
(ww)(iiiiii)(d){sss...}{L}

  () = required for all
  {} = required only for split/combined parcels


w = ward number
  (two string characters)
  (add leading zero if necessary, e.g. 01, 02, 03)
  
i = item number left of punctuation
  (six string characters)
  (add leading zero{es} if necessary, e.g. 000056, 003456, 000006)
  
d = punctuation
  (one and only one)
  (dash, "-", present if: {parcel created in a combine action})
  (dot, ".", present if:  {parcel created in a split action}; OR
                          parcel has been subject to neither a split nor a combine action *default*)
  
  s = item number suffix
    {required when parcel has been subject to a split or a combine}
    {suffix length varies according to number of parcels}
    {if preceded by dash: last parcel in combined range, e.g. "012345678." - "012345704." ==> "012345678-704"}
    {if preceded by dot: number assigned sequentially to fractional parcel}
  
  L = last parcel in split sequence
