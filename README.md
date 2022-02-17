# sphinx-linenos-emphasize-lines-bug

Small example repository to show that the code block breaks when both `:linenos:` and `:emphasize-lines:` are used.
See <https://github.com/sphinx-doc/sphinx/issues/10203> for more information.

## Steps to reproduce the problem

1.  Install the requirements using `pip install .`.
2.  Run the `make html` command.
3.  See that the `highlighted` code lines are positioned under the line numbers.
