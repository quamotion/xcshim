set (xcode_version 11.0)
set (xcode_dir share/xcode/)

configure_file(xcodebuild.in xcodebuild @ONLY)
configure_file(carthage.in carthage @ONLY)
configure_file(xcrun.in xcrun @ONLY)
configure_file(Info.plist.in Info.plist @ONLY)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/xcodebuild DESTINATION ${xcode_dir})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/xcrun DESTINATION ${xcode_dir})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/carthage DESTINATION ${xcode_dir})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/Info.plist DESTINATION ${xcode_dir}/Contents/)
install(DIRECTORY DESTINATION ${xcode_dir}/Contents/Developer)

