# WindowsCMD

### Access to UNC

##### pushd <UNC path> will create a temporary virtual drive and get into it.
##### popd will delete the temporary drive and get you back to the path you were when you entered pushd.
C:\a\local\path> pushd \\network_host\a\network\path  
U:\a\network\path> REM a temporary U: virtual drive has been created  
U:\a\network\path> popd  
C:\a\local\path> REM the U: drive has been deleted  
C:\a\local\path>  
