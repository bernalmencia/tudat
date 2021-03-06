 #    Copyright (c) 2010-2017, Delft University of Technology
 #    All rigths reserved
 #
 #    This file is part of the Tudat. Redistribution and use in source and
 #    binary forms, with or without modification, are permitted exclusively
 #    under the terms of the Modified BSD license. You should have received
 #    a copy of the license with this file. If not, please or visit:
 #    http://tudat.tudelft.nl/LICENSE.


set(OBSERVABLECORRECTIONSDIR "${OBSERVATIONMODELSDIR}/ObservableCorrections")


# Set the source files.
set(OBSERVATION_MODELS_SOURCES
  "${SRCROOT}${OBSERVATIONMODELSDIR}/lightTimeSolution.cpp"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/observableTypes.cpp"
  "${SRCROOT}${OBSERVABLECORRECTIONSDIR}/firstOrderRelativisticLightTimeCorrection.cpp"
)

# Set the header files.
set(OBSERVATION_MODELS_HEADERS
  "${SRCROOT}${OBSERVATIONMODELSDIR}/angularPositionObservationModel.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/lightTimeSolution.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/linkTypeDefs.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/observableTypes.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/observationModel.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/observationBias.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/oneWayRangeObservationModel.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/positionObservationModel.h"
  "${SRCROOT}${OBSERVATIONMODELSDIR}/UnitTests/testLightTimeCorrections.h"
  "${SRCROOT}${OBSERVABLECORRECTIONSDIR}/lightTimeCorrection.h"
  "${SRCROOT}${OBSERVABLECORRECTIONSDIR}/firstOrderRelativisticLightTimeCorrection.h"
)


# Add static libraries.
add_library(tudat_observation_models STATIC ${OBSERVATION_MODELS_SOURCES} ${OBSERVATION_MODELS_HEADERS})
setup_tudat_library_target(tudat_observation_models "${SRCROOT}${OBSERVATIONMODELSDIR}")

if(USE_CSPICE)

    add_executable(test_LightTime "${SRCROOT}${OBSERVATIONMODELSDIR}/UnitTests/unitTestLightTimeSolution.cpp")
    setup_custom_test_program(test_LightTime "${SRCROOT}${OBSERVATIONMODELSDIR}")
    target_link_libraries(test_LightTime tudat_observation_models tudat_ephemerides tudat_basic_astrodynamics tudat_spice_interface ${SPICE_LIBRARIES} ${Boost_LIBRARIES})

    add_executable(test_AngularPositionModel "${SRCROOT}${OBSERVATIONMODELSDIR}/UnitTests/unitTestAngularPositionModel.cpp")
    setup_custom_test_program(test_AngularPositionModel "${SRCROOT}${OBSERVATIONMODELSDIR}")
    target_link_libraries(test_AngularPositionModel ${TUDAT_ESTIMATION_LIBRARIES} ${Boost_LIBRARIES})

    add_executable(test_OneWayRangeModel "${SRCROOT}${OBSERVATIONMODELSDIR}/UnitTests/unitTestOneWayRangeObservationModel.cpp")
    setup_custom_test_program(test_OneWayRangeModel "${SRCROOT}${OBSERVATIONMODELSDIR}")
    target_link_libraries(test_OneWayRangeModel ${TUDAT_ESTIMATION_LIBRARIES} ${Boost_LIBRARIES})

    add_executable(test_PositionObservationModel "${SRCROOT}${OBSERVATIONMODELSDIR}/UnitTests/unitTestPositionObservationModel.cpp")
    setup_custom_test_program(test_PositionObservationModel "${SRCROOT}${OBSERVATIONMODELSDIR}")
    target_link_libraries(test_PositionObservationModel ${TUDAT_ESTIMATION_LIBRARIES} ${Boost_LIBRARIES})

endif( )
