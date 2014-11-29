restclient(0.1.0) -- An erlang REST Client library
====================================

## NOTE

This is a fork of [https://github.com/kivra/restclient](https://github.com/kivra/restclient)

* Asynchronous request support was added.
* JSX was replaced by Jiffy -- JSON support.

## DESCRIPTION

restclient is a library to help with consuming RESTful web services. It supports
encoding and decoding JSON, Percent and XML and comes with a convenience
function for working with urls and query parameters.

## USAGE

Include restclient as a rebar dependency with:

	{deps, [{restc, ".*", {git, "https://github.com/cabol/restclient", {branch, "master"}}}]}.

Start erlang shell:

    # erl -pa ./ebin ./deps/*/ebin

Now you have to start inets before using the client and if you want to use https make sure to start ssl before.
Then you can use the client as:

``` erlang
	1> [application:start(X) || X <- [inets, crypto, asn1, public_key, ssl]].
	[ok,ok,ok,ok,ok]
	2> restc:request(get, json, "https://api.github.com", [], [{"User-Agent", "my-client"}]).
	{ok,200,
        [{"cache-control","public, max-age=60, s-maxage=60"},
         {"date","Sat, 29 Nov 2014 15:26:42 GMT"},
         {"etag","\"6054d411bfab71fbe263aa36308ef4f0\""},
         {"server","GitHub.com"},
         {"vary","Accept"},
         {"content-length","1780"},
         {"content-type","application/json; charset=utf-8"},
         {"status","200 OK"},
         {"x-ratelimit-limit","60"},
         {"x-ratelimit-remaining","58"},
         {"x-ratelimit-reset","1417278331"},
         {"x-github-media-type","github.v3"},
         {"x-xss-protection","1; mode=block"},
         {"x-frame-options","deny"},
         {"content-security-policy","default-src 'none'"},
         {"access-control-allow-credentials","true"},
         {"access-control-expose-headers",
          "ETag, Link, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval"},
         {"access-control-allow-origin","*"},
         {"x-github-request-id","BAB12F30:0F97:24821A2:5479E5A2"},
         {"strict-transport-security",
          "max-age=31536000; includeSubdomains; preload"},
         {"x-content-type-options","nosniff"},
         {"x-served-by","4c8b2d4732c413f4b9aefe394bd65569"}],
        {[{<<"current_user_url">>,<<"https://api.github.com/user">>},
          {<<"authorizations_url">>,
           <<"https://api.github.com/authorizations">>},
          {<<"code_search_url">>,
           <<"https://api.github.com/search/code?q={query}{&page,per_page,sort,order}">>},
          {<<"emails_url">>,<<"https://api.github.com/user/emails">>},
          {<<"emojis_url">>,<<"https://api.github.com/emojis">>},
          {<<"events_url">>,<<"https://api.github.com/events">>},
          {<<"feeds_url">>,<<"https://api.github.com/feeds">>},
          {<<"following_url">>,
           <<"https://api.github.com/user/following{/target}">>},
          {<<"gists_url">>,
           <<"https://api.github.com/gists{/gist_id}">>},
          {<<"hub_url">>,<<"https://api.github.com/hub">>},
          {<<"issue_search_url">>,
           <<"https://api.github.com/search/issues?q={quer"...>>},
          {<<"issues_url">>,<<"https://api.github.com/issues">>},
          {<<"keys_url">>,<<"https://api.github.com/user/keys">>},
          {<<"notifications_url">>,
           <<"https://api.github.com/notificat"...>>},
          {<<"organization_repositories_url">>,
           <<"https://api.github.com/orgs/"...>>},
          {<<"organization_url">>,<<"https://api.github.com/o"...>>},
          {<<"public_gists_url">>,<<"https://api.github.c"...>>},
          {<<"rate_limit_url">>,<<"https://api.gith"...>>},
          {<<"repository_url">>,<<"https://api."...>>},
          {<<"repository_s"...>>,<<"https://"...>>},
          {<<"current_"...>>,<<"http"...>>},
          {<<"star"...>>,<<...>>},
          {<<...>>,...},
          {...}|...]}}
	3> restc:request(get, json, "https://api.github.com", [201], [{"User-Agent", "my-client"}]).
	{error,200,
           [{"cache-control","public, max-age=60, s-maxage=60"},
            {"date","Sat, 29 Nov 2014 15:29:04 GMT"},
            {"etag","\"6054d411bfab71fbe263aa36308ef4f0\""},
            {"server","GitHub.com"},
            {"vary","Accept"},
            {"content-length","1780"},
            {"content-type","application/json; charset=utf-8"},
            {"status","200 OK"},
            {"x-ratelimit-limit","60"},
            {"x-ratelimit-remaining","57"},
            {"x-ratelimit-reset","1417278331"},
            {"x-github-media-type","github.v3"},
            {"x-xss-protection","1; mode=block"},
            {"x-frame-options","deny"},
            {"content-security-policy","default-src 'none'"},
            {"access-control-allow-credentials","true"},
            {"access-control-expose-headers",
             "ETag, Link, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval"},
            {"access-control-allow-origin","*"},
            {"x-github-request-id","BAB12F30:6D6A:2683F09:5479E63E"},
            {"strict-transport-security",
             "max-age=31536000; includeSubdomains; preload"},
            {"x-content-type-options","nosniff"},
            {"x-served-by","2811da37fbdda4367181b328b22b2499"}],
           {[{<<"current_user_url">>,<<"https://api.github.com/user">>},
             {<<"authorizations_url">>,
              <<"https://api.github.com/authorizations">>},
             {<<"code_search_url">>,
              <<"https://api.github.com/search/code?q={query}{&page,per_page,sort,order}">>},
             {<<"emails_url">>,<<"https://api.github.com/user/emails">>},
             {<<"emojis_url">>,<<"https://api.github.com/emojis">>},
             {<<"events_url">>,<<"https://api.github.com/events">>},
             {<<"feeds_url">>,<<"https://api.github.com/feeds">>},
             {<<"following_url">>,
              <<"https://api.github.com/user/following{/target}">>},
             {<<"gists_url">>,
              <<"https://api.github.com/gists{/gist_id}">>},
             {<<"hub_url">>,<<"https://api.github.com/hub">>},
             {<<"issue_search_url">>,
              <<"https://api.github.com/search/issues?q={quer"...>>},
             {<<"issues_url">>,<<"https://api.github.com/issues">>},
             {<<"keys_url">>,<<"https://api.github.com/user/keys">>},
             {<<"notifications_url">>,
              <<"https://api.github.com/notificat"...>>},
             {<<"organization_repositories_url">>,
              <<"https://api.github.com/orgs/"...>>},
             {<<"organization_url">>,<<"https://api.github.com/o"...>>},
             {<<"public_gists_url">>,<<"https://api.github.c"...>>},
             {<<"rate_limit_url">>,<<"https://api.gith"...>>},
             {<<"repository_url">>,<<"https://api."...>>},
             {<<"repository_s"...>>,<<"https://"...>>},
             {<<"current_"...>>,<<"http"...>>},
             {<<"star"...>>,<<...>>},
             {<<...>>,...},
             {...}|...]}}
```

There's also convenience functions for working with urls and query string:

``` erlang
	7> restc:construct_url("http://www.example.com/te", "res/res1/res2", [{"q1", "qval1"}, {"q2", "qval2"}]).
	"http://www.example.com/te/res/res1/res2?q1=qval1&q2=qval2"
```

## License
The KIVRA restclient library uses an [MIT license](http://en.wikipedia.org/wiki/MIT_License). So go ahead and do what
you want!

Lots of fun!
