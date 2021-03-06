itk_module_test()
set(ITKIOGDCMTests
itkGDCMImageIOTest.cxx
itkGDCMImageIOTest2.cxx
itkGDCMImageIONoCrashTest.cxx
itkGDCMSeriesReadImageWrite.cxx
itkGDCMSeriesMissingDicomTagTest.cxx
itkGDCMSeriesStreamReadImageWrite.cxx
itkGDCMImagePositionPatientTest.cxx
itkGDCMImageIOOrthoDirTest.cxx
)

CreateTestDriver(ITKIOGDCM  "${ITKIOGDCM-Test_LIBRARIES}" "${ITKIOGDCMTests}")

itk_add_test(NAME itkGDCMImageIOTest1
      COMMAND ITKIOGDCMTestDriver itkGDCMImageIOTest
              DATA{${ITK_DATA_ROOT}/Input/dicom-sc_cs-1.dcm} ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest.dcm ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest.png ${ITK_TEST_OUTPUT_DIR}/itkGDCMRescaleImageIOTest.dcm)
itk_add_test(NAME itkGDCMImageIOTest2
      COMMAND ITKIOGDCMTestDriver itkGDCMImageIOTest
              DATA{${ITK_DATA_ROOT}/Input/itkGDCMImageIOTest.dcm} ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest2.dcm ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest2.png ${ITK_TEST_OUTPUT_DIR}/itkGDCMRescaleImageIOTest2.dcm)
itk_add_test(NAME itkGDCMImageIOTest3
      COMMAND ITKIOGDCMTestDriver itkGDCMImageIOTest
              DATA{${ITK_DATA_ROOT}/Input/012345.002.050} ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest3.dcm ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest3.png ${ITK_TEST_OUTPUT_DIR}/itkGDCMRescaleImageIOTest3.dcm)
itk_add_test(NAME itkGDCMImageIOTest4
      COMMAND ITKIOGDCMTestDriver itkGDCMImageIOTest
              DATA{${ITK_DATA_ROOT}/Input/itkGDCMImageIOTest3.dcm} ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest4.dcm ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest4.png ${ITK_TEST_OUTPUT_DIR}/itkGDCMRescaleImageIOTest4.dcm)
itk_add_test(NAME itkGDCMImageIOTest5
      COMMAND ITKIOGDCMTestDriver itkGDCMImageIOTest2
              DATA{${ITK_DATA_ROOT}/Input/HeadMRVolume.mhd,HeadMRVolume.raw} ${ITK_TEST_OUTPUT_DIR}/itkGDCMImageIOTest5)

itk_add_test(NAME itkGDCMSeriesReadImageWrite
      COMMAND ITKIOGDCMTestDriver itkGDCMSeriesReadImageWrite
              DATA{${ITK_DATA_ROOT}/Input/DicomSeries/,REGEX:Image[0-9]+.dcm}
              ${ITK_TEST_OUTPUT_DIR}/itkGDCMSeriesReadImageWrite.vtk ${ITK_TEST_OUTPUT_DIR})

set_property(TEST itkGDCMSeriesReadImageWrite APPEND PROPERTY DEPENDS ITKData)

itk_add_test(NAME itkGDCMSeriesStreamReadImageWrite1
      COMMAND ITKIOGDCMTestDriver itkGDCMSeriesStreamReadImageWrite
              DATA{${ITK_DATA_ROOT}/Input/DicomSeries/,REGEX:Image[0-9]+.dcm}
              ${ITK_TEST_OUTPUT_DIR}/itkGDCMSeriesStreamReadImageWrite1.mhd 0.859375 0.85939 1.60016 0)

set_property(TEST itkGDCMSeriesStreamReadImageWrite1 APPEND PROPERTY DEPENDS ITKData)

itk_add_test(NAME itkGDCMSeriesStreamReadImageWrite2
      COMMAND ITKIOGDCMTestDriver itkGDCMSeriesStreamReadImageWrite
              DATA{${ITK_DATA_ROOT}/Input/DicomSeries/,REGEX:Image[0-9]+.dcm}
              ${ITK_TEST_OUTPUT_DIR}/itkGDCMSeriesStreamReadImageWrite2.mhd 0.859375 0.85939 1.60016 1)

set_property(TEST itkGDCMSeriesStreamReadImageWrite2 APPEND PROPERTY DEPENDS ITKData)

itk_add_test(NAME itkGDCMImagePositionPatientTest
      COMMAND ITKIOGDCMTestDriver itkGDCMImagePositionPatientTest
              ${ITK_TEST_OUTPUT_DIR})

itk_add_test(NAME itkGDCMSeriesMissingDicomTagTest
  COMMAND ITKIOGDCMTestDriver itkGDCMSeriesMissingDicomTagTest
  DATA{${ITK_DATA_ROOT}/Input/DicomSeries2/,Image0075.dcm,Image0076-missingTag.dcm})

itk_add_test(NAME itkGDCMImageIOOrthoDirTest
  COMMAND ITKIOGDCMTestDriver itkGDCMImageIOOrthoDirTest
  DATA{${ITK_DATA_ROOT}/Input/OrthogonalDirectionsTest.dcm})

set_property(TEST itkGDCMSeriesMissingDicomTagTest APPEND PROPERTY DEPENDS ITKData)

itk_add_test(NAME itkGDCMImageIONoCrashTest
             COMMAND ITKIOGDCMTestDriver itkGDCMImageIONoCrashTest DATA{${ITK_DATA_ROOT}/Input/OT-PAL-8-face.dcm})
