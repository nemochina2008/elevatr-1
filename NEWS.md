elevatr 0.2.0 (2018-11-28)
==========================
# API Changes
- Major change for this is dropping Mapzen support since Mapzen shutdown in January of 2018.  Replacement services for terrain tiles exist at Nextzen, however; the published geotiff endpoints were not working.  I opted to not include the Nextzen endpoints at this time.  Rolled back to terrain tiles from AWS only.

# Added Functionality
- Added point elevations from AWS.  Extract point elevations from a DEM obtained via `get_elev_raster()`.  Will likely be faster for cases with many points in a relatively small geographic area.
- Added a clip argument to `get_elev_raster()`.  Default behavior of returning the full tiles is the same as in prior versions.  The argument expands this by allowing users to clip the resultant DEM either by the bounding box of the input locations via `clip = "bbox"` or by the locations themselves via `clip = "locations"`.  Partly inspired by https://github.com/jhollist/elevatr/issues/13.  Thanks to Michael Sumner (@mdsumner) for the inspiration.     
- Support for input simple features of the class `sf` has been added.  This is supported by coercion of the input `sf` class to a `SpatialXDataFrame`.  An `sf` object is also returned when used as the input locations for `get_elev_point`

# Minor Changes
- Updated Vignette to reflect new focus on AWS and USGS
- Updated Tests
- Updated README
- Added message to inform user of vertical units and CRS.


elevatr 0.1.4 (2017-12-28)
==========================
## Bug Fixes
- Primary change with this released is fixing a bug with the return file type on the AWS and mapzen APIs.  "tif" was changed to "tiff" and the check was stopping processing of the raster images.  Details are on <https://github.com/jhollist/elevatr/issues/17>. Thanks to the following individuals for catching this: @yipcma, @TomBor, @jslingsby.  And thanks to @vividbot for <https://github.com/jhollist/elevatr/pull/18> which provided a fix.  
- Thanks to @pascalfust for this issue: <https://github.com/USEPA/elevatr/issues/2>.  Kicked me into gear to send fix to CRAN.
- Fixed NOTE on CRAN: Packages in Imports, not imported.
    - Removed prettyunits
    - moved rgdal to suggests
    - Changed where ratelimitr getting called (was not in a function so couldn't be exported/called.
- Fixed travis build errors caused by change in elevation API that now requires a key.
- Added deprecation message to get_elev_point and get_elev_raster, due to pending shutdown of Mapzen :(

elevatr 0.1.2 (2017-03-13)
==========================

## Bug Fix
- There was a typo in building the mapzen api key.  Was masked prior as a keyless access was allowed.  It no longer is and get_elev_raster was failing.  That has been fixed
- Tests also failing due to keyless access.  Encripted key now pushed for use on travis.  Tests not run on CRAN
- Thanks to @hrbrmstr for pointing me in the right direction on fixing the testing with an api key.
- Also thanks to @noamross and @ropensci for maintaing <https://discuss.ropensci.org> where I found <https://discuss.ropensci.org/t/test-api-wrapping-r-packages-with-oauth-tokens/157>.  And thanks to @jennybc for wrapping all this up and provide great guidance on testing and vignettes that require a key.  That info is here: <https://rawgit.com/jennybc/googlesheets/master/vignettes/managing-auth-tokens.html#encrypting-tokens-for-hosted-continuous-integration>


elevatr 0.1.1 (2017-01-27)
==========================

## Minor Changes
- inst/doc was inadvertently included in package.  This verisons removes that and includes only vignettes.


elevatr 0.1.0 (2017-01-25)
==========================

## Initial CRAN Release
- This is the initial CRAN release. Provides access to point elevation data from USGS and from Mapzen.  Provides access to raster DEM from Mapzen Terrain Tiles and AWS Terrain Tiles.