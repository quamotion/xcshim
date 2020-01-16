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

# This is currently broken for DEB packages. It looks like the package generator follows symlinks (at least for directories),
# which is not what we want here.
# execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink ../../opt/xcode/Contents/Developer ${CMAKE_CURRENT_BINARY_DIR}/xcode_dir_link)
# install(FILES ${CMAKE_CURRENT_BINARY_DIR}/xcode_dir_link DESTINATION /usr/share/xcode-select/)

execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink ../opt/xcode/xcrun ${CMAKE_CURRENT_BINARY_DIR}/xcrun_symlink)
execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink ../opt/xcode/carthage ${CMAKE_CURRENT_BINARY_DIR}/carthage_symlink)
execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink ../opt/xcode/xcodebuild ${CMAKE_CURRENT_BINARY_DIR}/xcodebuild_symlink)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/xcrun_symlink RENAME xcrun DESTINATION ${CMAKE_INSTALL_PREFIX}/bin/)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/carthage_symlink RENAME carthage DESTINATION ${CMAKE_INSTALL_PREFIX}/bin/)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/xcodebuild_symlink RENAME xcodebuild DESTINATION ${CMAKE_INSTALL_PREFIX}/bin/)

install(DIRECTORY DESTINATION ${xcode_dir}/Contents/Developer)
install(DIRECTORY DESTINATION ${config_dir})
install(DIRECTORY DESTINATION ${developer_disk_dir})

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/10-xcshim.sh DESTINATION ${etc_dir}/profile.d)
