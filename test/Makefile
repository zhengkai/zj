SHELL:=/bin/bash

coverage = coverage.out

default:
	@sudo mkdir log-dir-deny
	@sudo chmod 0000 log-dir-deny
	@go test -v -test.bench=".*" -test.benchmem \
		-coverpkg github.com/zhengkai/zj -covermode=count -coverprofile="$(coverage)" \
		| GREP_COLORS="mt=1;92" grep --color=always -E '^(|PASS)' \
		| GREP_COLORS="mt=1;91" grep --color=always -E '^(|FAIL)'
	@if [ -n "$$COVERALLS_TOKEN" ]; then \
		"$$HOME/gopath/bin/goveralls" -coverprofile "$(coverage)" -service travis-ci -repotoken "$$COVERALLS_TOKEN" || : ; \
	fi

view:
	go tool cover -html="$(coverage)"

clean:
	@rm -rf log-dir
	@sudo rm -rf log-dir-deny
	@rm -f log-file
	@rm -f log-color
	@rm -f "$(coverage)"
