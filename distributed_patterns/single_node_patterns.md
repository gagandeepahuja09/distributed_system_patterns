Why do we need single-node patterns?
* It is much more clear on why would we want to break our application into different container running on different machines? 
* But why would we want to break up the components running on a single machine into different containers?
    1. Establishing boundaries around specific resources. (e.g this application needs two cores and 8 GB of memory).
    2. Boundaries help in providing team ownership.
    3. Provide separation of concerns. (eg. this image does this one thing.)