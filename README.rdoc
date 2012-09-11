=== Setup

I deliberately committed the .bundle directory so the gems will stay in the
current directory, even though I don't normally commit that.

First run ```bundle install --path gems```

Once that completes, run ```mv gems gems2 ; ln -s gems2 gem``` to make sure the gem
path is a symlink.

Then to replicate the bug, simply run ```bundle exec ruby test.rb```

My ruby is ```ruby 1.9.3p194 (2012-04-20 revision 35410) [x86_64-linux]``` using rbenv.

The "bug" can be fixed by making sure all gems wrap any constant declaration
around an ```if``` block so it doesn't get defined twice. Most gems, including
multi_json seem to do this, although I am not sure why they bother since in
theory it should not be necessary.
