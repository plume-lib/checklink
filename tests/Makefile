all: python-style-check python-typecheck test

PYTHON_FILES:=../checklink-persistent-errors
python-style-fix:
ifneq (${PYTHON_FILES},)
	@ruff format ${PYTHON_FILES}
	@ruff -q check ${PYTHON_FILES} --fix
endif
python-style-check:
ifneq (${PYTHON_FILES},)
	@ruff -q format --check ${PYTHON_FILES}
	@ruff -q check ${PYTHON_FILES}
endif
python-typecheck:
ifneq (${PYTHON_FILES},)
	@mypy --strict --install-types --non-interactive ${PYTHON_FILES} > /dev/null 2>&1 || true
	mypy --strict --ignore-missing-imports ${PYTHON_FILES}
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
