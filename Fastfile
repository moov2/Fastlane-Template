# Moov2 Fastlane example file

fastlane_version "1.40.0"

default_platform :ios

platform :ios do

  before_all do
    # ENV["SLACK_URL"] = "https://hooks.slack.com/services/..."
    # increment_build_number
  end


  desc "This will update/download and install provisional profile for development"
  lane :dev do

    sigh(
      adhoc: false,
      development: true,
      # provisioning_name: "***", #Name of existing developer provisional if there is any
      output_path: ENV["SIGH_OUTPUT_DIRECTORY"],
      force: true
    )

  end


  desc "Submit a new Beta Build to Fabric users"
  lane :beta do
    
    sigh(
      adhoc: true,
      # provisioning_name: "***", #Name of existing ad-hoc provisional if there is any
      output_path: ENV["SIGH_OUTPUT_DIRECTORY"],
      force: true
    )

    cocoapods

    gym(
      workspace: ENV["WORKSPACE"],
      scheme: ENV["SCHEME"],
      clean: true,
      output_directory: ENV["OUTPUT_DIRECTORY"],
      output_name: ENV["SCHEME"] + ".ipa",
      export_method: 'ad-hoc'
    )

    crashlytics(
      crashlytics_path: 'Pods/Crashlytics/Crashlytics.framework',
      api_token: ENV["FABRIC_API_KEY"],
      build_secret: ENV["FABRIC_BUILD_SECRET"],
      ipa_path: ENV["OUTPUT_DIRECTORY"] + "/" + ENV["SCHEME"] + ".ipa",
      # notes: "", # Release note
      groups: ENV["FABRIC_GROUP"],
    )

  end



  desc "Deploy a new version to the App Store"
  lane :deploy do

    sigh(
      adhoc: false,
      # provisioning_name: "***", #Name of existing App Store provisional if there is any
      output_path: ENV["SIGH_OUTPUT_DIRECTORY"]
    )

    cocoapods

    gym(
      workspace: ENV["WORKSPACE"],
      scheme: ENV["SCHEME"],
      clean: true,
      output_directory: ENV["OUTPUT_DIRECTORY"],
      output_name: ENV["SCHEME"] + ".ipa",
      export_method: 'app-store'
    )

    deliver(
      force: true,
    )

  end

  after_all do |lane|
    # This block is called, only if the executed lane was successful
    
    # slack(
    #   message: "Successfully deployed new App Update."
    # )
  end

  error do |lane, exception|
    # slack(
    #   message: exception.message,
    #   success: false
    # )
  end
end
