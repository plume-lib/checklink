.PHONY: all test clean prek
all: prek test

PYTHON_FILES:=../checklink-persistent-errors
prek:
ifneq (${PYTHON_FILES},)
	prek -q run ${PYTHON_FILES}
endif

test: errors1.output errors2.output
	diff errors1.output-goal errors1.output
	diff errors2.output-goal errors2.output

errors1.output: ../checklink-persistent-errors
	$< errors1.txt 3 > $@

errors2.output: ../checklink-persistent-errors
	$< errors2.txt 2 > $@

clean:
	rm -f errors1.output errors2.output
