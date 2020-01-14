# Lesson Setup

**WORK IN PROGRESS.  If you are reading this and the lessons prior to the workshop, things will be broken and incomplete.**

These notebooks are designed to run on the https://jupyter.nersc.gov but the serial portion of the notebooks should run anywhere that TOAST is installed.  You can set up these notebooks completely within the jupyter session.

## Browsing the Output

If you are browsing through the lessons on github, the notebooks will not be rendered and all their output is stripped to avoid polluting the git history.  A rendered version of the notebooks is available here:

https://portal.nersc.gov/project/cmb/toast-workshop-tokyo-2020/

## Connect to Jupyterhub

Make sure you have activated your NERSC account and [have set up MFA](https://www.nersc.gov/users/connecting-to-nersc/mfa/).  Then go to <https://jupyter.nersc.gov> and log in.  Select a "shared cori node" to run your session.  You should now be at a file system browser.  

## Clone this Repo

Go to the Jupyter menu File-->New-->Terminal.  This will launch a terminal window.  Decide where you want to put it and then clone this repo (you can **paste** into the JupyterLab terminal with `ctrl-shift-V` or invoking the contextual menu with `shift-rightclick`):

    git clone https://github.com/hpc4cmb/toast-workshop-tokyo-2020

## Set Up Your Software Stack

Before running these notebooks, we need to install a custom ipython kernel.  This only needs to be done when the software stack is updated.  From the terminal, load the latest "cmbenv" software stack:

    module use /global/common/software/cmb/cori/default/modulefiles

    module load cmbenv

    source cmbenv

Now there will be a command available which installs the kernel for this stack:

    cmbenv-jupyter

## Open a Lesson

In the jupyter file browser, navigate to the workshop git checkout and go into
`lessons/01_Introduction`.  Double click on the `intro.ipynb` file to open it.  Under
the Run menu, select "Run all".  You can repeat this for the other notebooks.

# Developer Notes

This git repository has a hook which runs the `nbstripout` tool on notebooks when
committing.  You will need to have that tool installed (via pip or conda) to commit
changes to the notebooks.  You should then go into this git repo and do:

    nbstripout --install

If you want to update the rendered notebooks, connect to NERSC's jupyter lab.  Then open
each notebook and "Run all" cells.  Note that this may submit interactive jobs, etc,
which is why we don't automate the execution of all notebooks on conversion.  After the
notebooks are all run and the output is generated, open a jupyter terminal and run the
lessons/render.py script.  This will export all notebooks to html and copy them to the
web-visible directory.
