project('FlowFields', ['cpp','c'],
  version : '0.1',
  default_options : ['warning_level=3', 'cpp_std=c++14'])

project_dir = meson.current_source_dir()
build_dir = meson.current_build_dir()

inc = [include_directories('Libraries/include'), include_directories('include')]

cpp = meson.get_compiler('cpp')
c = meson.get_compiler('c')

source_files = ['main.cpp', 'glad.c']

deps = []
args = []

host_system = host_machine.system()
if host_system == 'windows'
  # Undefined references without this one
  deps += cpp.find_library('glfw3dll', dirs : project_dir / 'Libraries/lib', static : true)
  deps += cpp.find_library('glfw3', dirs : project_dir / 'Libraries/lib', static : true)
  deps += cpp.find_library('glut32', dirs : project_dir / 'Libraries/lib', static : true)
  deps += cpp.find_library('glut32', dirs : project_dir / 'Libraries/lib', static : false)
  deps += dependency('GL')
  

elif host_system == 'darwin'
  deps += dependency('GL')
  deps += cpp.find_library('libglfw.3.3', dirs : project_dir + '/Libraries/lib', static : false)
  args = ['-framework','GLUT']

elif host_system == 'linux'
  deps += dependency('GL')
  deps += cpp.find_library('glfw', dirs : project_dir / 'Libraries/lib')
endif

install_data(project_dir / 'Libraries/lib/glfw3.dll')
install_subdir(project_dir / 'Libraries', install_dir : '')

#install_subdir(project_dir / 'shaders', install_dir: build_dir, strip_directory : false)
#install_subdir(project_dir / 'sprites', install_dir: build_dir, strip_directory : false)
install_data(project_dir / 'Libraries/lib/glfw3.dll', install_dir: build_dir)

#subdir('include')
#subdir('dependencies')
#subdir('source')

exe = executable('FlowFields', source_files,
    include_directories : inc,
    dependencies : deps,
    install : false,
    link_args : args)

#pkg_mod = import('pkgconfig')
#pkg_mod.generate(libraries : glBase,
#                 version : '1.0.0',
#                 name : 'glBase',
#                 filebase : 'glBase',
#                 description : 'A base program for using OpenGL.')

                 