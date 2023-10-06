# My Copy of the Fluent Python 2nd Edition Code

My intention at this point is to keep all of my modifications in the branch `greywidget`.

I've left the example notebook files under version control for now, but I think if I play with them I will always `git restore` them back to the original form. Since I'll probably play with this code on both my Windows and my Mac machines, I don't want to mess around with changes due to `EOL` difference between Windows and Mac. (I think there are ways to manage this but I've never quite sorted it out)

For now, the only dependency is to `python -m pip install notebook` which at the time of writing is version 7.0.4 which I've pinned in my `requirements.in` file. Oh, and PyTest

Note that for now I'm running `pip-compile` with the recommended flag: `pip-compile --strip-extras`

My intention is to work through this with the group on the PyBites PDM program.