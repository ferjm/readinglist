SERVER_URL = http://localhost:8000
VIRTUALENV=virtualenv
VENV := $(shell echo $${VIRTUAL_ENV-.venv})
PYTHON=$(VENV)/bin/python

TEST_SUITE = loadtest.TestBasic.test_all

# Hackety-hack around OSX system python bustage.
# The need for this should go away with a future osx/xcode update.
ARCHFLAGS = -Wno-error=unused-command-line-argument-hard-error-in-future
INSTALL = ARCHFLAGS=$(ARCHFLAGS) $(VENV)/bin/pip install

.PHONY: install clean bench megabench

$(PYTHON):
	virtualenv $(VENV)


# Build virtualenv, to ensure we have all the dependencies.
.env.install: $(PYTHON)
	$(INSTALL) git+git://github.com/mozilla-services/loads.git  >> loadtest.log && \
	rm loadtest.log || cat loadtest.log
	touch $@

install: .env.install

# Clean all the things installed by `make build`.
clean:
	rm -rf .venv *.pyc .env.install

# Run a single test from the venv machine, for sanity-checking.
test: install
	$(VENV)/bin/loads-runner --config=./config/test.ini --server-url=$(SERVER_URL) $(TEST_SUITE)

# Run a bench of 20 concurrent users.
bench:
	$(VENV)/bin/loads-runner --config=./config/bench.ini --server-url=$(SERVER_URL) $(TEST_SUITE)

# Run a much bigger bench, by submitting to broker in AWS.
megabench:
	$(VENV)/bin/loads-runner --config=./config/megabench.ini --user-id=$(USER) --server-url=$(SERVER_URL) $(TEST_SUITE)

smoke:
	$(VENV)/bin/loads-runner --config=./config/smoke.ini --user-id=$(USER) --server-url=$(SERVER_URL) $(TEST_SUITE)

# Purge any currently-running loadtest runs.
purge:
	$(VENV)/bin/loads-runner --config=./config/megabench.ini --purge-broker

attach:
	$(VENV)/bin/loads-runner --config=./config/megabench.ini --attach
