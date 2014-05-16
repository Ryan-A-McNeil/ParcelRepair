ParcelRepair
============

Transforms a City of Detroit parcel number (or its constituent ward and item numbers) into the format prescribed by the assessment units in Detroit and Wayne County.

The script will fix most common formatting errors (i.e. insufficient number of leading zeroes and missing punctuation), but cannot correct human error. Once I’ve run the script, I’ll usually compare the results against the assessor’s parcel numbers to identify any rogue mismatched parcel numbers. These are usually limited to data entry problems (e.g. digit transposition) or selection of an alternate tax ID for a given address, and can generally be corrected by comparing addresses to a reference data set (e.g. assessor’s parcel and address list). Any revised parcel numbers without a match on this list will need to be addressed on a case-by-case basis, but these are typically limited to a manageable number.

This method expects full parcel numbers (stored as strings, not numbers) for the input arguments. If your data have only Ward and Item numbers, you’ll need to concatenate those fields prior to running the transformation. If your Ward numbers do not have a leading zero, that is not a problem as the script will correct that as necessary. Output parcel numbers will be formatted as string values.

Be sure to update your worksheet and the columns within the code to reflect your data (these lines are commented to remind you).


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
