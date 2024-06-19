# example-percy-playwright-python
Example repo for demonstrating Percy Web/Percy on Automate integration with python using playwright.

## Python Playwright Tutorial

The tutorial assumes you're already familiar with Python and
[Playwright](https://playwright.dev/) and focuses on using it with Percy. You'll still
be able to follow along if you're not familiar with Python, Playwright, but we won't
spend time introducing Python, Playwright concepts.

The tutorial also assumes you have [Node 16+ with
npm](https://nodejs.org/en/download/) and
[git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) installed.

### Step 1

Clone the example application and install dependencies:

Minimum required `@percy/cli` version is `1.28.8-beta.3` onwards for this to work correctly. If you already have `@percy/cli` installed please update it to latest or minium required version.

```bash
$ git clone https://github.com/percy/example-percy-playwright-python.git
$ cd example-percy-playwright-python

# create virtual environment
$ python3 -m venv env
$ source env/bin/activate

# update the pip if not updated already using [python3 -m pip install --upgrade pip]
# install the required packages
$ pip3 install -r requirements.txt
$ npm install
```

This tutorial specifically uses Browserstack Automate for Percy on Automate to run playwright test.
For Percy Web you can run the scripts directly after setting up PERCY_TOKEN.

**Note:** In case of web we are using local browser feel free to update them as per you requirement. You don't need Browserstack Automate setup for the same.
For automate you will need credentials so refer to following instructions to get the same.

1. You will need a BrowserStack `username` and `access key`. To obtain your access credentials, [sign up](https://www.browserstack.com/users/sign_up?utm_campaign=Search-Brand-India&utm_source=google&utm_medium=cpc&utm_content=609922405128&utm_term=browserstack) for a free trial or [purchase a plan](https://www.browserstack.com/pricing).

2. Please get your `username` and `access key` from [profile](https://www.browserstack.com/accounts/profile) page.

### Step 2

Sign in to Percy and create a new **Automate** project under **Web** category. You can name the project "test-project" if you'd like. After
you've created the project, you'll be shown a token environment variable.

### Step 3

In the shell window you're working in, export the token and other environment variable:

**PERCY_TOKEN** is used by percy to identify the project and create the builds.

**Note:** In case of web projects, token will start with ***web_*** keyword.
**Note:** In case of automate projects, token will start with ***auto_*** keyword.

**Unix**

``` shell
$ export PERCY_TOKEN="<your token here>"
```

**Windows**

``` shell
$ set PERCY_TOKEN="<your token here>"

# PowerShell
$ $Env:PERCY_TOKEN="<your token here>"
```

Set the necessary **BROWSERSTACK ENVIRONMENT** variables, **only required for Percy on Automate examples**

**Unix**

``` shell
$ export BROWSERSTACK_USERNAME="<your browserstack user_name>"
$ export BROWSERSTACK_ACCESS_KEY="<your browserstack access_key>"
```

**Windows**

``` shell
$ set BROWSERSTACK_USERNAME="<your browserstack access_key>"
$ set BROWSERSTACK_ACCESS_KEY="<your browserstack access_key>"

# PowerShell
$ $Env:BROWSERSTACK_USERNAME="<your browserstack access_key>"
$ $Env:BROWSERSTACK_ACCESS_KEY="<your browserstack access_key>"
```

Alternatively you can also update `USER_NAME`, `ACCESS_KEY` with Browserstack User name, Access key in the script as well.


### Step 4

Considering all the above steps are done, we will run our tests, which will create automate session as well as percy build.

#### For Percy Web
**Note:** In case of web we are using local browser feel free to update them as per you requirement. You don't need automate setup for the same.

``` shell
$ npx percy exec -- python3 tests/web/test.py
```

Your **First Percy Web** build is created.
On completion of the script, you would be able to see the your percy build. Since we ran for the first time, we would see these are new screenshots and hence there would be no comparisons.

#### For Percy on Automate

``` shell
$ npx percy exec -- python3 tests/automate/test.py
```

Your **First Percy on Automate** build is created.
On completion of the script, you would be able to see the your percy build. Since we ran for the first time, we would see these are new screenshots and hence there would be no comparisons.


### Step 5

Now in order to make comparisons happen we need to make changes to the existing website so that a visual change can occur you can go to file in `test.py` and make changes.
Or else just run `after_test.py`, we have already made visual changes in this script. If you run the `after_test.py` script in tests, this would create few visual changes and would get compared to the last build and we would be able to see few diffs.

#### For Percy Web

``` shell
$ npx percy exec -- python3 tests/web/after_test.py
```

#### For Percy on Automate

``` shell
$ npx percy exec -- python3 tests/automate/after_test.py
```

On completion of this script, this build would get compared to the previous build and hence we can see the visual changes which percy detected.

### Finished! 😀

From here, you can try making your own changes to the website and functional tests, if you like. If you do, re-run the tests and you'll see any visual changes reflected in Percy.
