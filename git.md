[alias]
	last = !git reflog | grep checkout | sed -n \"s/.* to //p\" | uniq | head -n 10
