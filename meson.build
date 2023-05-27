project(
    'starter-project',
    'cpp',
    default_options: [
        'buildtype=release',
        'optimization=3',
        'strip=true',
        'cpp_std=c++11',
        'b_ndebug=if-release',
    ],
)

deps = []
deps += dependency('oatpp', version: '1.3.0', default_options: ['tests=false'])


starter_lib = library(
    'starter',
    files(
        'src/AppComponent.hpp',
        'src/controller/MyController.cpp',
        'src/controller/MyController.hpp',
        'src/dto/DTOs.hpp',
    ),
    include_directories: include_directories('src'),
    dependencies: deps,
    override_options: ['warning_level=3', 'werror=false'],
)


executable(
    'starter',
    files('src/App.cpp', 'test/app/MyApiTestClient.hpp'),
    include_directories: include_directories('src'),
    dependencies: deps,
    link_with: starter_lib,
    override_options: ['warning_level=3', 'werror=false'],
)


if get_option('tests')

    test_deps = deps
    test_deps += dependency('oatpp-test', version: '1.3.0')

    starter_test = executable(
        'starter_test',
        files(
            'test/MyControllerTest.cpp',
            'test/MyControllerTest.hpp',
            'test/app/MyApiTestClient.hpp',
            'test/app/TestComponent.hpp',
            'test/tests.cpp',
        ),
        include_directories: include_directories('test', 'src'),
        link_with: starter_lib,
        dependencies: test_deps,
        override_options: ['warning_level=1', 'werror=false'],
    )
    test('Starter Tests', starter_test)

endif
