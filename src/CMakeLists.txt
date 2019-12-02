set (etc_dir /etc)

set (xcode_version 11.0)
set (xcode_dir ${CMAKE_INSTALL_PREFIX}/opt/xcode)

set (config_dir ${etc_dir}/quamotion)
set (license_file ${config_dir}/.license)
set (developer_profile_file ${config_dir}/quamotion.developerprofile)
set (developer_profile_password quamotion)
set (developer_disk_dir ${config_dir}/devimg)

configure_file(xcodebuild.in xcodebuild @ONLY)
configure_file(carthage.in carthage @ONLY)
configure_file(xcrun.in xcrun @ONLY)
configure_file(Info.plist.in Info.plist @ONLY)
configure_file(10-xcshim.sh.in 10-xcshim.sh @ONLY)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/xcodebuild DESTINATION ${xcode_dir} PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/xcrun DESTINATION ${xcode_dir} PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/carthage DESTINATION ${xcode_dir} PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/Info.plist DESTINATION ${xcode_dir}/Contents/)
install(DIRECTORY DESTINATION ${xcode_dir}/Contents/Developer)
install(DIRECTORY DESTINATION ${config_dir})
install(DIRECTORY DESTINATION ${developer_disk_dir})

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/10-xcshim.sh DESTINATION ${etc_dir}/profile.d)
