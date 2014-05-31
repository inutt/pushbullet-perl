Net::PushBullet
===============

A pushbullet API library for perl.


Usage
-----

	use Net::PushBullet;

	my $p = Net::PushByllet->new(
		api_key => <api key>, # can also use key_file to provide a filename to a file that contains the key
		device_id => <iden value for device to push to> # optional, leave out to push to all your devices
	);


Device management
-----------------

Example responses in PushBullet's API documentation at http://docs.pushbullet.com/v2/devices/

	$devices = $p->get_devices();
	$p->delete_device($iden); # $iden value obtained from the device list


Pushing
-------

All calls return push details as per http://docs.pushbullet.com/v2/pushes/

	$p->push_note("Title", "Message");

	$p->push_link("Title", "URL");
	$p->push_link("Title", "URL", "Message);

	$p->push_address("Title", "1-13 St Giles High Street, London WC2H 8AG"); # Address provided can be approximate - it's just passed as a search to google maps (or similar)

	$p->push_list("Title", "Item 1", "Item 2", "Item 3", ...);
	$p->push_list("Title", @list);

	$p->push_file("/path/to/file"); # 25MB limit on maximum file size at the time of writing

Pushing things to contacts isn't supported yet, but probably will be eventually.


Deleting pushes
---------------

	$p->delete_push($iden); # $iden value returned by push_ functions

Deleting a push also removes the notification from mobile devices if not already dismissed.


User info
---------

	$me = $p->get_user(); # Get info for your account
	@contacts = $p->get_contacts(); # Get list of your contacts
