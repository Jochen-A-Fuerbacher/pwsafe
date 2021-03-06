include(CheckLibraryExists)

set (CORE_SRCS
  AES.cpp
  BlowFish.cpp
  CheckVersion.cpp
  Command.cpp
  CoreImpExp.cpp
  CoreOtherDB.cpp
  ExpiredList.cpp
  ItemAtt.cpp
  Item.cpp
  ItemData.cpp
  ItemField.cpp
  KeyWrap.cpp
  Match.cpp
  pbkdf2.cpp
  PWCharPool.cpp
  PWHistory.cpp
  PWPolicy.cpp
  PWSAuxParse.cpp
  PWScore.cpp
  PWSdirs.cpp
  PWSfile.cpp
  PWSfileHeader.cpp
  PWSfileV1V2.cpp
  PWSfileV3.cpp
  PWSfileV4.cpp
  PWSFilters.cpp
  PWSLog.cpp
  PWSprefs.cpp
  PWSrand.cpp
  PWStime.cpp
  Report.cpp
  sha1.cpp
  sha256.cpp
  StringX.cpp
  SysInfo.cpp
  TwoFish.cpp
  UnknownField.cpp
  UTF8Conv.cpp
  Util.cpp
  VerifyFormat.cpp
  XMLprefs.cpp
  XML/Xerces/XFileSAX2Handlers.cpp
  XML/Xerces/XFileValidator.cpp
  XML/Xerces/XFileXMLProcessor.cpp
  XML/Xerces/XFilterSAX2Handlers.cpp
  XML/Xerces/XFilterXMLProcessor.cpp
  XML/Xerces/XSecMemMgr.cpp
  XML/XMLFileHandlers.cpp
  XML/XMLFileValidation.cpp
  pugixml/pugixml.cpp
  )

if (NOT WIN32)
  list (APPEND CORE_SRCS ${CMAKE_CURRENT_BINARY_DIR}/core_st.cpp)
  
  set (RC2CPP "${PROJECT_SOURCE_DIR}/Misc/rc2cpp.pl")

  add_custom_command (
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/core_st.cpp ${CMAKE_CURRENT_BINARY_DIR}/core_st.h
    COMMAND ${RC2CPP} ${PROJECT_SOURCE_DIR}/src/core/core.rc2
    COMMAND "mv"  ${PROJECT_SOURCE_DIR}/src/core/core_st.cpp  ${CMAKE_CURRENT_BINARY_DIR}/core_st.cpp
    COMMAND "mv"  ${PROJECT_SOURCE_DIR}/src/core/core_st.h  ${CMAKE_CURRENT_BINARY_DIR}/core_st.h
    DEPENDS core.rc2
    )
  include_directories(${CMAKE_CURRENT_BINARY_DIR})
else ()
  list (APPEND CORE_SRCS core.rc2)
endif()

add_library(core ${CORE_SRCS})
