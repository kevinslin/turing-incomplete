require 'yaml'

class Mp3Details
  attr_accessor :file_size, :audio_length, :episode_number, :date

  def initialize
    load_config
    set_file_data
  end

  def set_file_data
    file = find_latest_file
    puts "******* #{file} ********"
    self.file_size = File.size file
    puts "* File Size: #{file_size}"
  end

  private

  def find_latest_file
    path = @config["mp3_directory"]
    regex = @config["mp3_prefix"]

    files = Dir.glob(File.join(path, '*.*'))
    files.select! { |f| f.to_s.match(regex) != nil }
    files.max { |a,b| File.ctime(a) <=> File.ctime(b) }
  end

  def load_config
    @config = YAML.load_file(".config.yml")
  rescue
    puts "Error loading config file. Please make sure there's a .config.yml in the project's root directory."
  end
end

task :metadata do
  details = Mp3Details.new
end
