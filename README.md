### Usual Stuff:

- bundle
- rake db:create db:migrate db:seed
- yarn install
- ./bin/webpack-dev-server
- rails s

## Installation Dependencies

Core project dependencies are: Ruby, Yarn and PostgreSQL. The following versions were used for this set-up on a 64-bit Windows 10 machine:

- **[RubyInstaller](https://rubyinstaller.org/downloads/):** Ruby+Devkit 2.5.3-1 (x64) 
- **[Yarn](https://yarnpkg.com/lang/en/docs/install/#windows-stable):** Stable (1.13.0) `.msi` installer (NodeJS must have been first installed before running this installer)
- **[PostgreSQL](https://www.postgresql.org/download/windows):** version 10.7 

### Installation Instructions

1. Install [Ruby](https://www.ruby-lang.org/en/). For windows machines, use the [RubyInstaller](https://rubyinstaller.org/downloads/).
	- select `Ruby+Devkit 2.5.3-1 (x64)`. Install all `MSYS2 toolchain` when prompted.

2. Install the Ruby Bundler. Open a command line and run the following commands. Do not overwrite if these they are already available:
	- `gem install bundler`

4. Install [Yarn](https://yarnpkg.com/lang/en/docs/install/#windows-stable).

5. Install PostgreSQL.



## Project Set-up

As of this date (20190219), the original project files will need to be updated:

1. Open the `Gemfile`.
	- Update the ruby version. Ruby 2.5.3 was used for this set-up. Overwrite with: `ruby '2.5.3'`
	- Add `gem 'tzinfo-data'` 

2. Open a command line and navigate to your project directory. Run `bundle` from the command line.

3. Run `yarn install`.

3. Open and connect to PostgreSQL.

4. Open `/config/database.yml`. Delete the `database` line under `development`, `test` and `production`. Replace with <br> 

	`url: postgres://postgres:admin@localhost/storybook`. (where "storybook" is the database name. You can assign your own DB name). Delete the `username` and `password` lines under `production`.

5. Open `/db/seeds.rb`. Delete all `private: true` nodes.

6. Open a command line and navigate to your project directory. Run `rake db:create db:migrate db:seed`


## Running the Project

Open (2) instances of the command line and navigate both to your project directory.

1. In command line (1), run `ruby bin/webpack-dev-server`.

2. In command line (2), run `rails s`.

3. Open a web browser and load `http://localhost:3000` (use the IP from `rails s`).



## Troubleshooting Rails

**"Could not open library 'libcurl': The specified module could not be found"**

1. Download cURL from the following URL: [https://curl.haxx.se/windows/](https://curl.haxx.se/windows/) (Choose 64bit if that's the system you're using). [[mirror here](https://www.dropbox.com/s/jed2dnjvjshwrfo/curl-7.64.0-win64-mingw.zip?dl=0)].

2. Go into the archive and browse to `/bin`
Locate `libcurl_x64.dll` (it may be just `libcurl.dll`)
Extract to your local drive.

3. Rename it to `libcurl.dll` if it has the `_x64` suffix
Cut + paste the file into the `/bin` directory of your Ruby installation