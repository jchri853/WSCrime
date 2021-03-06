# -*- coding: utf-8 -*-
$:.unshift("/Library/RubyMotion/lib")
require 'motion/project'
require 'bundler'
Bundler.setup
Bundler.require

Motion::Project::App.setup do |app|
  app.name = 'W-S Crime'
  app.identifier = 'com.mohawkapps.Winston-Salem-Crime'
  app.frameworks += ['CoreLocation', 'MapKit', 'QuartzCore', 'AVFoundation', 'CoreGraphics']
  app.device_family = [:iphone, :ipad]
  app.version = '9'
  app.short_version = '1.6'
  app.interface_orientations = [:portrait, :landscape_left, :landscape_right, :portrait_upside_down]
  app.deployment_target = "5.1"
  app.info_plist['APP_STORE_ID'] = 472546582

  #Add Flurry Analytics as a static library.
  app.vendor_project('vendor/Flurry', :static,
    :products => ['libFlurry.a'],
    :headers_dir => 'vendor/Flurry')
  
  #app.vendor_project('vendor/ARKit/ARKit', :static)
  app.vendor_project('vendor/ARKit', :xcode,
    :headers_dir => 'ARKitLib/ARKit')

  app.pods do
    pod 'CKCalendar'
    pod 'Appirater'
  end

  app.development do
    app.entitlements['get-task-allow'] = true
    app.codesign_certificate = "iPhone Developer: Mark Rickert (YA2VZGDX4S)"
    app.provisioning_profile = "./Provisioning/WSCMDevelop.mobileprovision"  
  end

  app.release do
    app.codesign_certificate = "iPhone Distribution: Mohawk Apps, LLC"
    app.provisioning_profile = "./Provisioning/WSCMDistribute.mobileprovision"  
  end

end

desc "Open latest crash log"
task :log do
  app = Motion::Project::App.config
  exec "less '#{Dir[File.join(ENV['HOME'], "/Library/Logs/DiagnosticReports/#{app.name}*")].last}'"
end

# Rake helper tasks

desc "Run simulator in retina mode"
task :retina do
  exec "bundle exec rake simulator retina=true"
end

desc "Run simulator on iPad"
task :ipad do
  exec "bundle exec rake simulator device_family=ipad"
end

desc "Run simulator on iPad in retina mode"
task :ipadretina do
  exec "bundle exec rake simulator retina=true device_family=ipad"
end
