# CheckEmailAddress

|  |                                                             |
|-----------------|--------------------------------------------------------------------------|
| Implementation | User identity                                                            |
| Description    | Block the creation of accounts if certain email-address criteria are met |
| Author(s)      | Mirko Schiefelbein (Naitsirktalk)                                        |
| Latest version | 1.0 (2017-02-27)                                                         |
| MediaWiki      | 1.17+                                                                    |
| License        | GNU General Public License 2.0 or later                                  |

The [CheckEmailAddress](https://www.mediawiki.org/wiki/Extension:CheckEmailAddress) extension checks the email-address during the registration
process. It aims at preventing spammers from creating an account on wikis which
require email confirmation. CheckEmailAddress basically provides two features:

-   check the domain of the email-address: If it matches a certain provider-address, e.g. a known trash-email-address, account
creation fails, and the user is asked to register with a different email-address.
-   check the name of the email-address: If the name meets certain criteria,
account creation fails, and the user is asked to provide a different email-address.

Installation
------------

To install this extension, add the following to [LocalSettings.php]:

``` php
require_once("$IP/extensions/CheckEmailAddress/CheckEmailAddress.php");
$wgCheckEmailAddressDomainSources = array(
'type'  => CEASRC_FILE,
'src'   => "$IP/Blacklistfile.txt"
);
$wgCheckEmailAddressNameSigns = array(
array(
'sign'      => ".",
'maxcount'  => 5,
),
);
```

Create a textfile “**Blacklistfile.txt**”. Fill in domains of email-addresses that are
known as trash- or once-only-mails, e.g. mailinator.com. Just write the domains you
want to disable one below the other, without “@”. It should look something like this:

`mailinator.com`
`spoofmail.de`
`...`

Save Blacklistfile.txt in your root. *Note: the root directory of your
MediaWiki installation is the same directory that holds [LocalSettings.php]*.

### Configuration parameters

#### $wgCheckEmailAddressDomainSources

This is a simple array that informs what *type* the source is and which
*sourcefile* is used. At the moment only “CEASRC\_FILE” is possible
as “type”. Point “src” to the file containing the email-addresses.

#### $wgCheckEmailAddressNameSigns

This array defines the signs and their limit in the name-part of the email-address, i.e. in
the part before “@”. Since this variable is an array of arrays, you can name several signs
with different limits. If for example known spammers keep registring with characteristic
email-names, you can now exclude them by patterns. In the configuration given above, email-names
are searched for dots (“.”). If they count equal or more than five, account creation fails.

[below]: #Code "wikilink"
[$IP]: Manual:$IP "wikilink"
[LocalSettings.php]: Manual:LocalSettings.php "wikilink"
