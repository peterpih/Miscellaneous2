Useful links:  
<b>setup</b>: http://sourabhbajaj.com/mac-setup/Heroku/README.html  
[pg:push and pg:pull]posgres</b>: https://devcenter.heroku.com/articles/heroku-postgresql#pg-push-and-pg-pull  
**git deploy**: https://dashboard.heroku.com/apps/aqueous-spire-6633/deploy/heroku-git   
**pulling down database**: 


###Install Heroku
On OSX, use Homebrew:  
<pre>
<b>brew install heroku-toolbelt</b>
<b>heroku update</b>
</pre>

###Heroku Commands  
<b>heroku local</b>             <em>( run the app locally from heroku )</em>

add <b>--app <em>APP</em></b> to specify non default Heroku <em>APP</em>  
<pre>
<b>heroku open</b>              <em>( open a link to the app website in local browser )</em>
<b>heroku ps</b>                <em>( dynos running on Heroku )</em>

<em>( show configuration vars and the database url )</em>
<b>heroku config</b>            


<b>heroku addons</b>            <em>( show additional services )</em>

<b>heroku pg:psql</b>           <em>( for <a href="#accessing-database-remotely">postgres on Heroku</a> )</em>

<em>( dump one or more tables from a database )</em>
<b>heroku pg:dump -t</b> <em>table-name [-t database-name] database-name</em>

<em>( take site down / up for maintenance )</em>
<b>heroku maintenance:on</b>    
<b>heroku maintenance:off</b>

<em>( show log file for Heroku APP )</em>
<b>heroku logs --app</b> <em>APP</em> 

<em>( show nlines in log file for Heroku APP )</em>
<b>heroku logs --app</b> <em>APP</em> <b>-n</b> <em>nlines</em>  

<em>( tail the logs )</em>
<b>heroku logs --app</b> <em>APP</em> <b>--tail</b> 


<b>heroku restart --app</b> <em>APP</em>             <em>( restart APP )</em>

<b>heroku run bash --app</b> <em>APP</em>            <em>( remote Unix command line )</em>
</pre>
  
###Example Heroku website
<pre>
<em>( clone a local repo from heroku )</em>
<b>heroku git:clone -a</b> <em>heroku_app</em> <em>dest_dir</em>

<em>( get the example app )</em>
<b>git clone https://github.com/heroku/ruby-getting-started.git</b> 

<b>heroku create</b>                       <em>( link to Heroku )</em>

<b>git push heroku master</b> <em>branch</em><b>:master</b> <em>( deploy app to Heroku git )</em>
<b>heroku open</b>                         <em>( open the website in a local browser )</em>
</pre>

###Papertrail
<pre>
<b>heroku addons</b>                       <em>( show addons )</em>
<b>heroku addons:doc papertrail</b>        <em>( documentation for papertrail )</em>
<b>heroku addons:open papertrail</b>       <em>( open a dashboard for papertrail )</em>

<b>heroku run bash</b>                     <em>( runs a remote shell )</em>
<b>heroku run</b> <em>command</em>                  <em>( runs a commandline command )</em>
<b>heroku run bundle install</b>
<b>heroku run rake db:migrate</b>

<b>heroku config</b>                       <em>( show config settings )</em>
                                    <em>( database url is shown here )</em>
<b>heroku config:set TIMES=10</b>          <em>( set TIMES env var to 10 )</em>
</pre>

###Postgres on Heroku  
NOTE: <b>DATABASE_URL</b> and <b>DATABASE</b> are the <b>literal strings</b> not env variables  
<pre>
<b>heroku pg:info</b>                      <em>( show some info about the database )</em>

<b>heroku pg:reset DATABASE_URL</b>        <em>( empties the database <b>DO NOT DELETE THE DATABASE</b></em>
                                    <em>( empty it using this )</em>

<b>heroku pg:credentials DATABASE</b>      <em>( shows the database credentials: username, password)</em>

<b>git push heroku test:master</b>         <em>( push 'test' branch to 'master' on heroku )</em>

<b>heroku pg:push</b> <em>mylocaldb</em> <b>DATABASE_URL</b>
<em>heroku pg:push mylocaldb HEROKU_POSTGRESQL_MAGENTA --app sushi</em>
</pre>

###To pull down a database:
<pre>
<b>heroku pg:pull</b>
<b>heroku pg:pull</b> <em>AMBER fff_development</em> <b>--app</b> <em>forever-family-foundation</em>
</pre>

<id='accessing-database-remotely'>
###Accessing database remotely
Need to be made a Collaborator on the database, then:  
<pre>
<b>heroku pg:psql --app</b> <em>APP</em>  
<b>heroku pg:psql --app</b> <em>aqueous-spire-6633</em>
</pre>
**Records created since 1 month ago**  
<pre>
<b>SELECT * FROM</b> <em>table-name</em> <b>WHERE</b> <em>column-name</em> > <b>CURRENT_DATE - INTERVAL '1 month';</b>
</pre>
###Production Check  
On the **Heroku  Dashboard**, click on hamburger in upper right-hand corner, then click **Production Check**
