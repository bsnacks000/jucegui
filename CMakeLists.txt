cmake_minimum_required(VERSION 3.15)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED 17)

project(juceplay VERSION 0.1.0)

add_subdirectory(JUCE)

# This follows this CMakeAPI guide
# https://github.com/juce-framework/JUCE/blob/master/examples/CMake/GuiApp/CMakeLists.txt

# Generate a gui app
juce_add_gui_app(JuceGUI
    COMPANY_NAME "bsnacks000"
    PRODUCT_NAME "JuceGUI"
)

# add our sources
target_sources(JuceGUI 
    PRIVATE 
        main.cpp 
        maincomponent.cpp
)


# Preprocessor defs
target_compile_definitions(JuceGUI
    PRIVATE 
        JUCE_WEB_BROWSER=0 
        JUCE_USE_CURL=0 
        JUCE_APPLICATION_NAME_STRING="$<TARGET_PROPERTY:JuceGUI,JUCE_PRODUCT_NAME>"
        JUCE_APPLICATION_VERSION_STRING="$<TARGET_PROPERTY:JuceGUI,JUCE_VERSION>"
)


# This adds binary data...
#juce_add_binary_data(JuceGUIAppData SOURCES ...)


target_link_libraries(JuceGUI
    PRIVATE
        juce::juce_gui_extra 
    PUBLIC 
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags
)


