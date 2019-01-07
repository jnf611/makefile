# General syntax:
#
#       target … : prerequisites …
#       	recipe
#
# - recipe are (shell ?) commands require to update the target
# - recipe is done if
#   - the target does not exist
#   - one of the prerequisites is newer than the targer
# - before doing recipe, Make execute all rules of the prerequisites

# Variables:
# - should not contain ‘:’, ‘#’, ‘=’, or whitespace
# - if local, should be lower case
src_dir = src
out_dir = out
executable = $(out_dir)/edit
objects = $(out_dir)/main.o $(out_dir)/tool.o

# First rule defines the default goal,
# e.g. the target Make will try to achieve without argument
default_goal: $(executable)
	echo "this is the default goal"

$(executable) : $(objects)
	cc -o $(executable) $(objects)

$(out_dir):
	mkdir -p $(out_dir)

$(out_dir)/main.o : $(src_dir)/main.c $(src_dir)/defs.h $(out_dir)/tool.h $(out_dir)
	cc -o $(out_dir)/main.o -c $(src_dir)/main.c

$(out_dir)/tool.o : $(src_dir)/tool.c $(src_dir)/defs.h $(out_dir)
	cc -o $(out_dir)/tool.o -c $(src_dir)/tool.c

# Implicit rule: the above could be written like this, since the the rule to
# compile a file.c to file.o is implicit to make
# (TODO: does this only work in the same folder ?)
#          main.o : defs.h
#
# Rules could also be regrouped by prerequisites:
#          $(objects): defs.h
#          main.o: tool.h

# TODO: - before rule should avoid failure, this doesn't work ?
clean :
	-rm -r $(out_dir)

