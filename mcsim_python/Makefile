# python don't have dependencies thus this is a workaround
.PHONY: environment remove-env install uninstall test # .PHONY is something we can add when our target dependencies are not files.

# define commonly used variables
MODULE=mcsim
ENVIRONMENT=chem274A_lab1

# Before running `conda` recipes, makefile runs the specified dependencies.
# So in this case makefile runs remove-env target prior to running the recipes.
# The first recipe creates a new python3.9 conda environment, named "chem274A_lab1".
# The second recipe installs several libraries from conda-forge repository into 
# the "chem274A_lab1" environment.
environment: remove-env
	conda create -n $(ENVIRONMENT) "python=3.9" --yes
	conda install -c conda-forge notebook nbconvert numpy matplotlib pytest-cov pandas --name $(ENVIRONMENT) --yes

# This target has no dependencies thus makefile will just run the recipe.
# The recipe removes the newly created environment. 
# Apparently the --all flag is required when removing environments.
# Alternative syntax: conda env remove --name $(ENVIRONMENT) 
remove-env:
	conda remove --name $(ENVIRONMENT) --all --yes

# Before running the target recipes, makefile runs uninstall target.
# After, the pip command installs the `mcsim` package
# This assumes that the makefile will be run in the mcsim_python directory
install: uninstall ## install the package to the active Python's site-packages
	pip install .

# Before running the target recipes, makefile runs uninstall target.
# After, the pip command installs the `mcsim` package and makes it editable
dev-install: uninstall
	pip install -e .

# This target has no dependencies thus makefile will just run the recipe.
# The pip command uninstalls the `mcsim`
uninstall: ## uninstall the package
	pip uninstall --yes $(MODULE)

# This target has no dependencies thus makefile will just run the recipe.
# The command runs pytest in the current directory
test: 
	pytest -v
