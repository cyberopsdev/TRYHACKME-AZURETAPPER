
usr-11216086@201618.onmicrosoft.com (Reader)  ──► Recon your environment and looking for Owner or Contributor (check on InfoNote)
                    ↓
App which we can escalate our privilege (UserAuthenticationMethod.ReadWrite.All) ──► Reset app password to login as an app to get the permisson to MODIFY Authentication Method 
                                                                                                                                 ↓
                                                                                          Set up TAP for users which has the access to network and VM (check users in InfoNote)
                                                                                                                                 ↓
                                                                                                         Read ProtectedSettings and decryted to get the flag 
