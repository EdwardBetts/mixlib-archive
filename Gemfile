source "https://rubygems.org"

gemspec name: "mixlib-archive"

# need the extract=to-destination support in ffi-libarchive 1.0.17
gem "ffi-libarchive", ">= 1.0.17"

group :test do
  gem "chefstyle", "1.6.2"
  gem "rake"
  gem "rspec", "~> 3.0"
  gem "parallel", "~> 1.20.1" #pin until we support ruby 2.4
end

group :debug do
  gem "pry"
  gem "pry-byebug"
  gem "rb-readline"
end

# These lines added for Windows (x64) development only.
# For ffi-libarchive to function during development on Windows we need the
# binaries in the RbConfig::CONFIG["bindir"]
#
# We copy (and overwrite) these files every time "bundle <exec|install>" is
# executed, just in case they have changed.
if RUBY_PLATFORM =~ /mswin|mingw|windows/
  instance_eval do
    ruby_exe_dir = RbConfig::CONFIG["bindir"]
    assemblies = Dir.glob(File.expand_path("distro/ruby_bin_folder", Dir.pwd) + "/*.dll")
    FileUtils.cp_r assemblies, ruby_exe_dir, verbose: false unless ENV["_BUNDLER_LIBARCHIVE_DLLS_COPIED"]
    ENV["_BUNDLER_LIBARCHIVE_DLLS_COPIED"] = "1"
  end
end
