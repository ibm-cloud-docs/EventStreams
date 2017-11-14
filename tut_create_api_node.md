





<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">

<meta content="origin-when-cross-origin" name="referrer" />

  <link crossorigin="anonymous" href="https://assets.github.ibm.com/assets/frameworks-81a59bf26d881d29286674f6deefe779c444382fff322085b50ba455460ccae5.css" integrity="sha256-gaWb8m2IHSkoZnT23u/necREOC//MiCFtQukVUYMyuU=" media="all" rel="stylesheet" />
  <link crossorigin="anonymous" href="https://assets.github.ibm.com/assets/github-b4d5077bdf40a2543c1ba5d7b6b44d2922fed22e58cea8f7c0949bd4c2925fcb.css" integrity="sha256-tNUHe99AolQ8G6XXtrRNKSL+0i5Yzqj3wJSb1MKSX8s=" media="all" rel="stylesheet" />
  
  
  
  

  <meta name="viewport" content="width=device-width">
  
  <title>apiconnect/tut_create_api_node.md at staging · Bluemix-Docs/apiconnect</title>
  <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
  <link rel="fluid-icon" href="https://github.ibm.com/fluidicon.png" title="GitHub">
  <meta property="fb:app_id" content="1401488693436528">

    
    <meta content="https://avatars.github.ibm.com/u/93385?s=400" property="og:image" /><meta content="GitHub Enterprise" property="og:site_name" /><meta content="object" property="og:type" /><meta content="Bluemix-Docs/apiconnect" property="og:title" /><meta content="https://github.ibm.com/Bluemix-Docs/apiconnect" property="og:url" /><meta content="apiconnect - staging" property="og:description" />

  <link rel="assets" href="https://assets.github.ibm.com/">
  <link rel="web-socket" href="wss://github.ibm.com/_sockets/VjI6NTc2MDk1MzplZWY5NjZkMGI2MGVhNzBjZmQ4ZWJmMWQ5MDBkYzkxMzJmMWRkZDlhMDJiNzc3YTc2YzVlZDExM2Y2MTM3MjU3--ef5f30b2fe9d1763f9b4758d94da89eea61cb18c">
  <meta name="pjax-timeout" content="1000">
  <link rel="sudo-modal" href="/sessions/sudo_modal">
  <meta name="request-id" content="9d9f9383-09df-4c7f-8804-65bab5f056ee" data-pjax-transient>
  

  <meta name="selected-link" value="repo_source" data-pjax-transient>

  <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
<meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">


<meta content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" name="analytics-location" />




  <meta class="js-ga-set" name="dimension1" content="Logged In">


  

      <meta name="hostname" content="github.ibm.com">
  <meta name="user-login" content="karen-rodgers">



  <meta name="html-safe-nonce" content="b01c6feb08fd867be7f3989d7c18b98b22b170bb">

  <meta http-equiv="x-pjax-version" content="c8749e8138bddaf4f34dc15669664b10">
  

    
  <meta name="description" content="apiconnect - staging">
  <meta name="go-import" content="github.ibm.com/Bluemix-Docs/apiconnect git https://github.ibm.com/Bluemix-Docs/apiconnect.git">

  
  <link href="https://github.ibm.com/Bluemix-Docs/apiconnect/commits/staging.atom?token=AAAYYcoCC97MVC-JM0D_XIybWvivQtxbks64FsBrwA%3D%3D" rel="alternate" title="Recent Commits to apiconnect:staging" type="application/atom+xml">


    <link rel="canonical" href="https://github.ibm.com/Bluemix-Docs/apiconnect/blob/staging/tutorials/tut_create_api_node.md" data-pjax-transient>



  <link rel="mask-icon" href="https://assets.github.ibm.com/pinned-octocat.svg" color="#000000">
  <link rel="icon" type="image/x-icon" href="https://assets.github.ibm.com/favicon-enterprise.ico">

<meta name="theme-color" content="#1e2327">



  </head>

  <body class="logged-in enterprise env-production page-blob">
    


  <div class="position-relative js-header-wrapper ">
    <a href="#start-of-content" tabindex="1" class="accessibility-aid js-skip-to-content">Skip to content</a>
    <div id="js-pjax-loader-bar" class="pjax-loader-bar"><div class="progress"></div></div>

    
    
    



        
<div class="header" role="banner">
  <div class="container clearfix">
    <a class="header-logo-invertocat" href="https://github.ibm.com/" data-hotkey="g d" aria-label="Homepage" data-ga-click="Header, go to dashboard, icon:logo">
  <svg aria-hidden="true" class="octicon octicon-mark-github" height="32" version="1.1" viewBox="0 0 16 16" width="32"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
    <span class="header-logo-subbrand">Enterprise</span>
</a>


        <div class="header-search scoped-search site-scoped-search js-site-search" role="search">
  <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/Bluemix-Docs/apiconnect/search" class="js-site-search-form" data-scoped-search-url="/Bluemix-Docs/apiconnect/search" data-unscoped-search-url="/search" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <label class="form-control header-search-wrapper js-chromeless-input-container">
        <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/tut_create_api_node.md" class="header-search-scope no-underline">This repository</a>
      <input type="text"
        class="form-control header-search-input js-site-search-focus js-site-search-field is-clearable"
        data-hotkey="s"
        name="q"
        value=""
        placeholder="Search"
        aria-label="Search this repository"
        data-unscoped-placeholder="Search GitHub"
        data-scoped-placeholder="Search"
        autocapitalize="off">
        <input type="hidden" class="js-site-search-type-field" name="type" >
    </label>
</form></div>


      <ul class="header-nav float-left" role="navigation">
        <li class="header-nav-item">
          <a href="/pulls" aria-label="Pull requests you created" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:pulls context:user" data-hotkey="g p" data-selected-links="/pulls /pulls/assigned /pulls/mentioned /pulls">
            Pull requests
</a>        </li>
        <li class="header-nav-item">
          <a href="/issues" aria-label="Issues you created" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:issues context:user" data-hotkey="g i" data-selected-links="/issues /issues/assigned /issues/mentioned /issues">
            Issues
</a>        </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="https://gist.github.ibm.com/" data-ga-click="Header, go to gist, text:gist">Gist</a>
          </li>
      </ul>

    
<ul class="header-nav user-nav float-right" id="user-links">
  <li class="header-nav-item">
    

  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link tooltipped tooltipped-s js-menu-target" href="/new"
       aria-label="Create new…"
       data-ga-click="Header, create new, icon:add">
      <svg aria-hidden="true" class="octicon octicon-plus float-left" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 9H7v5H5V9H0V7h5V2h2v5h5z"/></svg>
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <ul class="dropdown-menu dropdown-menu-sw">
        
<a class="dropdown-item" href="/new" data-ga-click="Header, create new repository">
  New repository
</a>


<a class="dropdown-item" href="https://gist.github.ibm.com/" data-ga-click="Header, create new gist">
  New gist
</a>

  <a class="dropdown-item" href="/organizations/new" data-ga-click="Header, create new organization">
    New organization
  </a>



  <div class="dropdown-divider"></div>
  <div class="dropdown-header">
    <span title="Bluemix-Docs/apiconnect">This repository</span>
  </div>
    <a class="dropdown-item" href="/Bluemix-Docs/apiconnect/issues/new" data-ga-click="Header, create new issue">
      New issue
    </a>

      </ul>
    </div>
  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link name tooltipped tooltipped-sw js-menu-target" href="/karen-rodgers"
       aria-label="View profile and more"
       data-ga-click="Header, show menu, icon:avatar">
      <img alt="@karen-rodgers" class="avatar" src="https://avatars.github.ibm.com/u/6241?s=40" height="20" width="20">
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <div class="dropdown-menu dropdown-menu-sw">
        <div class="dropdown-header header-nav-current-user css-truncate">
          Signed in as <strong class="css-truncate-target">karen-rodgers</strong>
        </div>

        <div class="dropdown-divider"></div>

        <a class="dropdown-item" href="/karen-rodgers" data-ga-click="Header, go to profile, text:your profile">
          Your profile
        </a>
        <a class="dropdown-item" href="/karen-rodgers?tab=stars" data-ga-click="Header, go to starred repos, text:your stars">
          Your stars
        </a>
        <a class="dropdown-item" href="/explore" data-ga-click="Header, go to explore, text:explore">
          Explore
        </a>
        <a class="dropdown-item" href="https://help.github.com/enterprise/2.10/user" data-ga-click="Header, go to help, text:help">
          Help
        </a>

        <div class="dropdown-divider"></div>

        <a class="dropdown-item" href="/settings/profile" data-ga-click="Header, go to settings, icon:settings">
          Settings
        </a>

        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/logout" class="logout-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="wXkb/F9aO9vEveGJqc3xsikcKNAT27JGlC7HBmKDZu5JQMl/Y9o3fHgOmenU+FlPQIKGCMAbUafv3wS8TOkHnA==" /></div>
          <button type="submit" class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout">
            Sign out
          </button>
</form>      </div>
    </div>
  </li>
</ul>


    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/logout" class="sr-only right-0" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="bx0ZzPztYmAK7Ea/RjA8meBUbCmd7oGRtTHRu3F3e8XnJMtPwG1ux7ZfPt87BZRkicrC8U4uYnDOwBIBXx0atw==" /></div>
      <button type="submit" class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout">
        Sign out
      </button>
</form>  </div>
</div>


      

  </div>

  <div id="start-of-content" class="accessibility-aid"></div>

    <div id="js-flash-container">
</div>



  <div role="main">
        <div itemscope itemtype="http://schema.org/SoftwareSourceCode">
    <div id="js-repo-pjax-container" data-pjax-container>
        




    <div class="pagehead repohead instapaper_ignore readability-menu experiment-repo-nav">
      <div class="container repohead-details-container">

        <ul class="pagehead-actions">
  <li>
        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/notifications/subscribe" class="js-social-container" data-autosubmit="true" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="XMUThRH3Sxfh/3TUCsoxyfrHGHM3yMq74mLsBGl/L8UYYg8RG3NJN9alwujJYMGKLQToxG2N82l8o7eWRDV26Q==" /></div>      <input class="form-control" id="repository_id" name="repository_id" type="hidden" value="180952" />

        <div class="select-menu js-menu-container js-select-menu">
          <a href="/Bluemix-Docs/apiconnect/subscription"
            class="btn btn-sm btn-with-count select-menu-button js-menu-target" role="button" tabindex="0" aria-haspopup="true"
            data-ga-click="Repository, click Watch settings, action:blob#show">
            <span class="js-select-button">
                <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                Watch
            </span>
          </a>
            <a class="social-count js-social-count"
              href="/Bluemix-Docs/apiconnect/watchers"
              aria-label="4 users are watching this repository">
              4
            </a>

        <div class="select-menu-modal-holder">
          <div class="select-menu-modal subscription-menu-modal js-menu-content">
            <div class="select-menu-header js-navigation-enable" tabindex="-1">
              <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
              <span class="select-menu-title">Notifications</span>
            </div>

              <div class="select-menu-list js-navigation-container" role="menu">

                <div class="select-menu-item js-navigation-item selected" role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input checked="checked" id="do_included" name="do" type="radio" value="included" />
                    <span class="select-menu-item-heading">Not watching</span>
                    <span class="description">Be notified when participating or @mentioned.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                      Watch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input id="do_subscribed" name="do" type="radio" value="subscribed" />
                    <span class="select-menu-item-heading">Watching</span>
                    <span class="description">Be notified of all conversations.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                        Unwatch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input id="do_ignore" name="do" type="radio" value="ignore" />
                    <span class="select-menu-item-heading">Ignoring</span>
                    <span class="description">Never be notified.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-mute" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8 2.81v10.38c0 .67-.81 1-1.28.53L3 10H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h2l3.72-3.72C7.19 1.81 8 2.14 8 2.81zm7.53 3.22l-1.06-1.06-1.97 1.97-1.97-1.97-1.06 1.06L11.44 8 9.47 9.97l1.06 1.06 1.97-1.97 1.97 1.97 1.06-1.06L13.56 8l1.97-1.97z"/></svg>
                        Stop ignoring
                    </span>
                  </div>
                </div>

              </div>

            </div>
          </div>
        </div>
</form>
  </li>

  <li>
      <div class="js-toggler-container js-social-container starring-container ">
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/Bluemix-Docs/apiconnect/unstar" class="starred" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="ttIDnyGm09tS6pdInwpjNjDHHDnrEdrwBm01ghIDFOyR52DBeZlkN1QhCi9w68GlgWHdqeSV9B2lVPkhV2dJHQ==" /></div>
      <button
        type="submit"
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Unstar this repository" title="Unstar Bluemix-Docs/apiconnect"
        data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"/></svg>
        Unstar
      </button>
        <a class="social-count js-social-count" href="/Bluemix-Docs/apiconnect/stargazers"
           aria-label="0 users starred this repository">
          0
        </a>
</form>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/Bluemix-Docs/apiconnect/star" class="unstarred" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="o4o/MJWdmcbpkl3iKSNCYU2OC1cjYKX/hATkaB8aHg07FyUIT1cIHUtw5Bgn1m9uX0UQhdbLCG2RuviM/L33JA==" /></div>
      <button
        type="submit"
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Star this repository" title="Star Bluemix-Docs/apiconnect"
        data-ga-click="Repository, click star button, action:blob#show; text:Star">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"/></svg>
        Star
      </button>
        <a class="social-count js-social-count" href="/Bluemix-Docs/apiconnect/stargazers"
           aria-label="0 users starred this repository">
          0
        </a>
</form>  </div>

  </li>

  <li>
          <a href="#fork-destination-box" class="btn btn-sm btn-with-count"
              title="Fork your own copy of Bluemix-Docs/apiconnect to your account"
              aria-label="Fork your own copy of Bluemix-Docs/apiconnect to your account"
              rel="facebox"
              data-ga-click="Repository, show fork modal, action:blob#show; text:Fork">
              <svg aria-hidden="true" class="octicon octicon-repo-forked" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path fill-rule="evenodd" d="M8 1a1.993 1.993 0 0 0-1 3.72V6L5 8 3 6V4.72A1.993 1.993 0 0 0 2 1a1.993 1.993 0 0 0-1 3.72V6.5l3 3v1.78A1.993 1.993 0 0 0 5 15a1.993 1.993 0 0 0 1-3.72V9.5l3-3V4.72A1.993 1.993 0 0 0 8 1zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3 10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3-10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
            Fork
          </a>

          <div id="fork-destination-box" style="display: none;">
            <h2 class="facebox-header" data-facebox-id="facebox-header">Where should we fork this repository?</h2>
            <include-fragment src=""
                class="js-fork-select-fragment fork-select-fragment"
                data-url="/Bluemix-Docs/apiconnect/fork?fragment=1">
              <img alt="Loading" height="64" src="https://assets.github.ibm.com/images/spinners/octocat-spinner-128.gif" width="64" />
            </include-fragment>
          </div>

    <a href="/Bluemix-Docs/apiconnect/network" class="social-count"
       aria-label="3 users forked this repository">
      3
    </a>
  </li>
</ul>

        <h1 class="public ">
  <svg aria-hidden="true" class="octicon octicon-repo" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M4 9H3V8h1v1zm0-3H3v1h1V6zm0-2H3v1h1V4zm0-2H3v1h1V2zm8-1v12c0 .55-.45 1-1 1H6v2l-1.5-1.5L3 16v-2H1c-.55 0-1-.45-1-1V1c0-.55.45-1 1-1h10c.55 0 1 .45 1 1zm-1 10H1v2h2v-1h3v1h5v-2zm0-10H2v9h9V1z"/></svg>
  <span class="author" itemprop="author"><a href="/Bluemix-Docs" class="url fn" rel="author">Bluemix-Docs</a></span><!--
--><span class="path-divider">/</span><!--
--><strong itemprop="name"><a href="/Bluemix-Docs/apiconnect" data-pjax="#js-repo-pjax-container">apiconnect</a></strong>

</h1>

      </div>
      <div class="container">
        
<nav class="reponav js-repo-nav js-sidenav-container-pjax"
     itemscope
     itemtype="http://schema.org/BreadcrumbList"
     role="navigation"
     data-pjax="#js-repo-pjax-container">

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/Bluemix-Docs/apiconnect" class="js-selected-navigation-item selected reponav-item" data-hotkey="g c" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches /Bluemix-Docs/apiconnect" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-code" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M9.5 3L8 4.5 11.5 8 8 11.5 9.5 13 14 8 9.5 3zm-5 0L0 8l4.5 5L6 11.5 2.5 8 6 4.5 4.5 3z"/></svg>
      <span itemprop="name">Code</span>
      <meta itemprop="position" content="1">
</a>  </span>

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a href="/Bluemix-Docs/apiconnect/issues" class="js-selected-navigation-item reponav-item" data-hotkey="g i" data-selected-links="repo_issues repo_labels repo_milestones /Bluemix-Docs/apiconnect/issues" itemprop="url">
        <svg aria-hidden="true" class="octicon octicon-issue-opened" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M7 2.3c3.14 0 5.7 2.56 5.7 5.7s-2.56 5.7-5.7 5.7A5.71 5.71 0 0 1 1.3 8c0-3.14 2.56-5.7 5.7-5.7zM7 1C3.14 1 0 4.14 0 8s3.14 7 7 7 7-3.14 7-7-3.14-7-7-7zm1 3H6v5h2V4zm0 6H6v2h2v-2z"/></svg>
        <span itemprop="name">Issues</span>
        <span class="Counter">0</span>
        <meta itemprop="position" content="2">
</a>    </span>

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/Bluemix-Docs/apiconnect/pulls" class="js-selected-navigation-item reponav-item" data-hotkey="g p" data-selected-links="repo_pulls /Bluemix-Docs/apiconnect/pulls" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-git-pull-request" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M11 11.28V5c-.03-.78-.34-1.47-.94-2.06C9.46 2.35 8.78 2.03 8 2H7V0L4 3l3 3V4h1c.27.02.48.11.69.31.21.2.3.42.31.69v6.28A1.993 1.993 0 0 0 10 15a1.993 1.993 0 0 0 1-3.72zm-1 2.92c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zM4 3c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v6.56A1.993 1.993 0 0 0 2 15a1.993 1.993 0 0 0 1-3.72V4.72c.59-.34 1-.98 1-1.72zm-.8 10c0 .66-.55 1.2-1.2 1.2-.65 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
      <span itemprop="name">Pull requests</span>
      <span class="Counter">0</span>
      <meta itemprop="position" content="3">
</a>  </span>

    <a href="/Bluemix-Docs/apiconnect/projects" class="js-selected-navigation-item reponav-item" data-selected-links="repo_projects new_repo_project repo_project /Bluemix-Docs/apiconnect/projects">
      <svg aria-hidden="true" class="octicon octicon-project" height="16" version="1.1" viewBox="0 0 15 16" width="15"><path fill-rule="evenodd" d="M10 12h3V2h-3v10zm-4-2h3V2H6v8zm-4 4h3V2H2v12zm-1 1h13V1H1v14zM14 0H1a1 1 0 0 0-1 1v14a1 1 0 0 0 1 1h13a1 1 0 0 0 1-1V1a1 1 0 0 0-1-1z"/></svg>
      Projects
      <span class="Counter" >0</span>
</a>
    <a href="/Bluemix-Docs/apiconnect/wiki" class="js-selected-navigation-item reponav-item" data-hotkey="g w" data-selected-links="repo_wiki /Bluemix-Docs/apiconnect/wiki">
      <svg aria-hidden="true" class="octicon octicon-book" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M3 5h4v1H3V5zm0 3h4V7H3v1zm0 2h4V9H3v1zm11-5h-4v1h4V5zm0 2h-4v1h4V7zm0 2h-4v1h4V9zm2-6v9c0 .55-.45 1-1 1H9.5l-1 1-1-1H2c-.55 0-1-.45-1-1V3c0-.55.45-1 1-1h5.5l1 1 1-1H15c.55 0 1 .45 1 1zm-8 .5L7.5 3H2v9h6V3.5zm7-.5H9.5l-.5.5V12h6V3z"/></svg>
      Wiki
</a>


  <a href="/Bluemix-Docs/apiconnect/pulse" class="js-selected-navigation-item reponav-item" data-selected-links="pulse /Bluemix-Docs/apiconnect/pulse">
    <svg aria-hidden="true" class="octicon octicon-pulse" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M11.5 8L8.8 5.4 6.6 8.5 5.5 1.6 2.38 8H0v2h3.6l.9-1.8.9 5.4L9 8.5l1.6 1.5H14V8z"/></svg>
    Pulse
</a>
  <a href="/Bluemix-Docs/apiconnect/graphs" class="js-selected-navigation-item reponav-item" data-selected-links="repo_graphs repo_contributors /Bluemix-Docs/apiconnect/graphs">
    <svg aria-hidden="true" class="octicon octicon-graph" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M16 14v1H0V0h1v14h15zM5 13H3V8h2v5zm4 0H7V3h2v10zm4 0h-2V6h2v7z"/></svg>
    Graphs
</a>

</nav>

      </div>
    </div>

<div class="container new-discussion-timeline experiment-repo-nav">
  <div class="repository-content">

    
          

<a href="/Bluemix-Docs/apiconnect/blob/b9d1884692cbcb986826d9b50fe6828d361f5d4e/tutorials/tut_create_api_node.md" class="d-none js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:31df4ab0746503112a8cd18a9ca723fc -->

<div class="file-navigation js-zeroclipboard-container">
  
<div class="select-menu branch-select-menu js-menu-container js-select-menu float-left">
  <button class=" btn btn-sm select-menu-button js-menu-target css-truncate" data-hotkey="w"
    
    type="button" aria-label="Switch branches or tags" tabindex="0" aria-haspopup="true">
      <i>Branch:</i>
      <span class="js-select-button css-truncate-target">staging</span>
  </button>

  <div class="select-menu-modal-holder js-menu-content js-navigation-container" data-pjax>

    <div class="select-menu-modal">
      <div class="select-menu-header">
        <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
        <span class="select-menu-title">Switch branches/tags</span>
      </div>

      <div class="select-menu-filters">
        <div class="select-menu-text-filter">
          <input type="text" aria-label="Filter branches/tags" id="context-commitish-filter-field" class="form-control js-filterable-field js-navigation-enable" placeholder="Filter branches/tags">
        </div>
        <div class="select-menu-tabs">
          <ul>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="branches" data-filter-placeholder="Filter branches/tags" class="js-select-menu-tab" role="tab">Branches</a>
            </li>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="tags" data-filter-placeholder="Find a tag…" class="js-select-menu-tab" role="tab">Tags</a>
            </li>
          </ul>
        </div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="branches" role="menu">

        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


            <a class="select-menu-item js-navigation-item js-navigation-open selected"
               href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/tut_create_api_node.md"
               data-name="staging"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                staging
              </span>
            </a>
        </div>

          <div class="select-menu-no-results">Nothing to show</div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="tags">
        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


        </div>

        <div class="select-menu-no-results">Nothing to show</div>
      </div>

    </div>
  </div>
</div>

  <div class="BtnGroup float-right">
    <a href="/Bluemix-Docs/apiconnect/find/staging"
          class="js-pjax-capture-input btn btn-sm BtnGroup-item"
          data-pjax
          data-hotkey="t">
      Find file
    </a>
    <button aria-label="Copy file path to clipboard" class="js-zeroclipboard btn btn-sm BtnGroup-item tooltipped tooltipped-s" data-copied-hint="Copied!" type="button">Copy path</button>
  </div>
  <div class="breadcrumb js-zeroclipboard-target">
    <span class="repo-root js-repo-root"><span class="js-path-segment"><a href="/Bluemix-Docs/apiconnect"><span>apiconnect</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a href="/Bluemix-Docs/apiconnect/tree/staging/tutorials"><span>tutorials</span></a></span><span class="separator">/</span><strong class="final-path">tut_create_api_node.md</strong>
  </div>
</div>



  <div class="commit-tease">
      <span class="float-right">
        <a class="commit-tease-sha" href="/Bluemix-Docs/apiconnect/commit/ee71ace2a6decde52885f619f825879d08a7e8d2" data-pjax>
          ee71ace
        </a>
        <relative-time datetime="2017-11-03T18:08:55Z">Nov 3, 2017</relative-time>
      </span>
      <div>
        <img alt="@cdawson" class="avatar" height="20" src="https://avatars.github.ibm.com/u/4515?s=40" width="20" />
        <a href="/cdawson" class="user-mention" rel="contributor">cdawson</a>
          <a href="/Bluemix-Docs/apiconnect/commit/ee71ace2a6decde52885f619f825879d08a7e8d2" class="message" data-pjax="true" title="Adding version limit">Adding version limit</a>
      </div>

    <div class="commit-tease-contributors">
      <button type="button" class="btn-link muted-link contributors-toggle" data-facebox="#blob_contributors_box">
        <strong>2</strong>
         contributors
      </button>
          <a class="avatar-link tooltipped tooltipped-s" aria-label="cdawson" href="/Bluemix-Docs/apiconnect/commits/staging/tutorials/tut_create_api_node.md?author=cdawson"><img alt="@cdawson" class="avatar" height="20" src="https://avatars.github.ibm.com/u/4515?s=40" width="20" /> </a>
    <a class="avatar-link tooltipped tooltipped-s" aria-label="rmckinn" href="/Bluemix-Docs/apiconnect/commits/staging/tutorials/tut_create_api_node.md?author=rmckinn"><img alt="@rmckinn" class="avatar" height="20" src="https://avatars.github.ibm.com/u/5508?s=40" width="20" /> </a>


    </div>

    <div id="blob_contributors_box" style="display:none">
      <h2 class="facebox-header" data-facebox-id="facebox-header">Users who have contributed to this file</h2>
      <ul class="facebox-user-list" data-facebox-id="facebox-description">
          <li class="facebox-user-list-item">
            <img alt="@cdawson" height="24" src="https://avatars.github.ibm.com/u/4515?s=48" width="24" />
            <a href="/cdawson">cdawson</a>
          </li>
          <li class="facebox-user-list-item">
            <img alt="@rmckinn" height="24" src="https://avatars.github.ibm.com/u/5508?s=48" width="24" />
            <a href="/rmckinn">rmckinn</a>
          </li>
      </ul>
    </div>
  </div>

<div class="file">
  <div class="file-header">
  <div class="file-actions">

    <div class="BtnGroup">
      <a href="/Bluemix-Docs/apiconnect/raw/staging/tutorials/tut_create_api_node.md" class="btn btn-sm BtnGroup-item" id="raw-url">Raw</a>
        <a href="/Bluemix-Docs/apiconnect/blame/staging/tutorials/tut_create_api_node.md" class="btn btn-sm js-update-url-with-hash BtnGroup-item" data-hotkey="b">Blame</a>
      <a href="/Bluemix-Docs/apiconnect/commits/staging/tutorials/tut_create_api_node.md" class="btn btn-sm BtnGroup-item" rel="nofollow">History</a>
    </div>

        <a class="btn-octicon tooltipped tooltipped-nw"
           href="x-github-client://openRepo/https://github.ibm.com/Bluemix-Docs/apiconnect?branch=staging&amp;filepath=tutorials%2Ftut_create_api_node.md"
           aria-label="Open this file in GitHub Desktop"
           data-ga-click="Repository, open with desktop, type:windows">
            <svg aria-hidden="true" class="octicon octicon-device-desktop" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"/></svg>
        </a>

        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/Bluemix-Docs/apiconnect/edit/staging/tutorials/tut_create_api_node.md" class="inline-form js-update-url-with-hash" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="6yVzAfLoqEhzsh3uMJ5rLylmDuQwjL4AZWI3p6lfm/RCs2+vrkBerCQEUDdLmkHkAg8kV45Yqzw2XBypP15VkA==" /></div>
          <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
            aria-label="Fork this project and edit the file" data-hotkey="e" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-pencil" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"/></svg>
          </button>
</form>        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/Bluemix-Docs/apiconnect/delete/staging/tutorials/tut_create_api_node.md" class="inline-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="q5K7wCkxhDN59rT8tnPb7Yotsm7XvhAfCv1PFRvNXs5Tg989rfkU12Y5qJTLan1QHkAubn6FG8yOCjAdFVAm3Q==" /></div>
          <button class="btn-octicon btn-octicon-danger tooltipped tooltipped-nw" type="submit"
            aria-label="Fork this project and delete the file" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-trashcan" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M11 2H9c0-.55-.45-1-1-1H5c-.55 0-1 .45-1 1H2c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1v9c0 .55.45 1 1 1h7c.55 0 1-.45 1-1V5c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm-1 12H3V5h1v8h1V5h1v8h1V5h1v8h1V5h1v9zm1-10H2V3h9v1z"/></svg>
          </button>
</form>  </div>

  <div class="file-info">
      256 lines (207 sloc)
      <span class="file-info-divider"></span>
    14.9 KB
  </div>
</div>

  
  <div id="readme" class="readme blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="text"><table data-table-type="yaml-metadata">
  <thead>
  <tr>
  <th>copyright</th>

  <th>lastupdated</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div><table>
  <thead>
  <tr>
  <th>years</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div>2017</div></td>
  </tr>
  </tbody>
</table></div></td>

  <td><div>2017-11-03</div></td>
  </tr>
  </tbody>
</table>

<p>{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}</p>
<h1><a id="user-content-creating-an-api-in-nodejs" class="anchor" href="#creating-an-api-in-nodejs" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Creating an API in Node.js</h1>
<p><strong>Duration</strong>: 20 mins<br>
<strong>Skill level</strong>: Beginner</p>
<hr>
<h2><a id="user-content-objective" class="anchor" href="#objective" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Objective</h2>
<p>This tutorial guides you through creating an API in Node.js using the LoopBack framework. The tutorial describes how to:</p>
<ol>
<li>Create a new LoopBack project.</li>
<li>Add a new data source and model to a LoopBack project using the API Designer in the {{site.data.keyword.apiconnect_full}} toolkit.</li>
<li>Test your API endpoints using the API Designer Explore tool.</li>
</ol>
<hr>
<h2><a id="user-content-prerequisites" class="anchor" href="#prerequisites" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Prerequisites</h2>
<p>Before you begin, <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/tut_prereq_install_toolkit.html">install the {{site.data.keyword.apiconnect_short}} toolkit</a>. If the toolkit is already installed, ensure that you are running version 5.0.8.1, or later. You can verify this by entering the following command on the command-line:
<code>apic -v</code></p>
<hr>
<h2><a id="user-content-create-a-loopback-project" class="anchor" href="#create-a-loopback-project" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Create a Loopback project</h2>
<p>You can create a Loopback project using either the {{site.data.keyword.apiconnect_short}} developer toolkit command-line interface or the API Designer interface.</p>
<h3><a id="user-content-create-a-loopback-project-using-the-toolkit-command-line" class="anchor" href="#create-a-loopback-project-using-the-toolkit-command-line" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Create a LoopBack project using the toolkit command line</h3>
<p>To create a LoopBack project using the {{site.data.keyword.apiconnect_short}} toolkit command line, complete the following steps:</p>
<ol>
<li>From the command-line interface, enter the following command. It is used to create and manage LoopBack applications.
<div class="highlight highlight-source-shell"><pre>apic loopback</pre></div>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
For this tutorial, you will create a project called weather-data.</p>
</blockquote>
</li>
<li>At the prompt, enter <code>weather-data</code> as the project name and press <strong>Enter</strong>.
<div class="highlight highlight-source-shell"><pre><span class="pl-k">?</span> What<span class="pl-s"><span class="pl-pds">'</span>s the name of your application? weather-data</span></pre></div>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/important.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/important.png" alt="important" title="Important!" style="max-width:100%;"></a>
In general, a project name can contain any characters except blank space (" "), forward slash ("/"), ampersand ("&amp;"), at ("@"), plus ("+"), percent ("%"), and colon (":").</p>
</blockquote>
</li>
<li>Enter the name of the directory in which to create the project. Press <strong>Enter</strong> to use a directory with the same name as the project, or type a new name and press <strong>Enter</strong>.
<div class="highlight highlight-source-shell"><pre><span class="pl-k">?</span> Enter name of the directory to contain the project: weather-data</pre></div>
</li>
<li>Select the version of LoopBack to use. Choose the current production version: 3.x.
<div class="highlight highlight-source-shell"><pre><span class="pl-k">?</span> Which version of LoopBack would you like to use<span class="pl-k">?</span> 
2.x (long term support) 
<span class="pl-k">?</span> 3.x (current) </pre></div>
</li>
<li>Specify the kind of application that you want to create by using the arrow keys to select <strong>empty-server</strong>.
<div class="highlight highlight-source-shell"><pre><span class="pl-k">?</span> What kind of application <span class="pl-k">do</span> you have <span class="pl-k">in</span> mind<span class="pl-k">?</span> (Use arrow keys)
<span class="pl-k">?</span> empty-server (An empty LoopBack API, without any configured models or datasources) 
hello-world (A project containing a basic working example, including a memory database) 
notes (A project containing a basic working example, including a memory database)</pre></div>
</li>
<li>Press <strong>Enter</strong> to create an empty LoopBack API.</li>
</ol>
<p>The tool displays a number of messages as it creates the project directory and adds a number of directories and files to it. It also runs npm install to install all the project dependencies, as specified in package.json. This process creates a node_modules directory and might take some time.</p>
<p>An empty LoopBack project contains the following directories:</p>
<ul>
<li>server: contains server model and data source definitions, and other server code</li>
<li>definitions: contains YAML definition files</li>
<li>node_modules: created by node.js</li>
</ul>
<h3><a id="user-content-create-a-loopback-project-using-the-api-designer-interface" class="anchor" href="#create-a-loopback-project-using-the-api-designer-interface" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Create a LoopBack project using the API Designer interface</h3>
<p>To create a LoopBack project using the API Designer, complete the following steps:</p>
<ol>
<li>
<p>From the command-line interface, enter the following command to start the API Designer:</p>
<div class="highlight highlight-source-shell"><pre>apic edit</pre></div>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/api-designer-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/api-designer-1.png" alt="" style="max-width:100%;"></a></p>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
The above command initializes the {{site.data.keyword.apiconnect_short}} toolkit and launches the API Designer in the default browser when it is done.
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
In this tutorial, you will create a project called weather-data.</p>
</blockquote>
</li>
<li>
<p>If you have not previously pinned the UI navigation pane, click the Navigate to icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/navigate-to.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/navigate-to.png" alt="" style="max-width:100%;"></a>. The API Manager UI navigation pane opens. To pin the UI navigation pane, click the Pin menu icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/pinned.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/pinned.png" alt="" style="max-width:100%;"></a>.</p>
</li>
<li>
<p>In the side bar, click the Projects Plus icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/add-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/add-icon.png" alt="" style="max-width:100%;"></a>.</p>
</li>
<li>
<p>Click <strong>Create LoopBack Project</strong>. You'll see the **Add new LoopBack project ** dialog.</p>
</li>
<li>
<p>Select <strong>empty-server</strong> as the project template.</p>
</li>
<li>
<p>For <strong>LoopBack Version</strong>, select version 3.x (the current version).</p>
</li>
<li>
<p>Enter <code>weather-data</code> for the Display Name and Name fields.</p>
</li>
<li>
<p>For the <strong>Project Directory</strong>, select the <code>weather-data</code> folder created in step 1 by clicking the <strong>Browse</strong> button.
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/api-designer-2.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/api-designer-2.png" alt="" style="max-width:100%;"></a></p>
</li>
<li>
<p>Click <strong>Add</strong> to add the project.</p>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
A number of messages will be displayed in the <strong>Add new LoopBack project</strong> window as it creates the project directory and adds a number of directories and files to it. It also runs npm install to install all the project dependencies, as specified in package.json. This process creates a node_modules directory and might take some time.</p>
</blockquote>
<blockquote>
<p>An empty LoopBack project contains the following directories:</p>
</blockquote>
<ul>
<li>server: contains server model and data source definitions, and other server code</li>
<li>definitions: contains YAML definition files</li>
<li>node_modules: created by node.js</li>
</ul>
</li>
<li>
<p>Click <strong>Finished</strong> to close the <strong>Add new LoopBack project</strong> dialog box.</p>
</li>
<li>
<p>Exit <strong>API Designer</strong> by going back to the command line in step 1 and entering <code>Ctrl + C</code>.  Type <code>Y</code> to confirm the exit.</p>
</li>
<li>
<p>Close the browser session.</p>
</li>
</ol>
<hr>
<h2><a id="user-content-add-a-new-data-source-and-model" class="anchor" href="#add-a-new-data-source-and-model" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add a new data source and model</h2>
<p>To add a new model and data source to a LoopBack project using the API Designer, complete the following steps:</p>
<h3><a id="user-content-add-a-data-source" class="anchor" href="#add-a-data-source" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add a data source</h3>
<p>To add a new data source to a LoopBack project using the API Designer, complete the following steps.</p>
<ol>
<li>You must also create a LoopBack project (the "weather-data" project) as described in <code>Create a LoopBack project from the command line</code> and make sure the current working directory is the project root directory:
<div class="highlight highlight-source-shell"><pre><span class="pl-c1">cd</span> weather-data</pre></div>
</li>
<li>From the command line, enter the following command:
<div class="highlight highlight-source-shell"><pre>apic edit</pre></div>
After a brief pause, the console displays this message:
<div class="highlight highlight-source-shell"><pre>Express server listening on http://127.0.0.1:9000</pre></div>
The API Designer opens in your default web browser, initially displaying the login page if you haven't logged in recently.
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
You can log in using your Bluemix account or create one.</p>
</blockquote>
</li>
<li>Click the <strong>Data Sources</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/datasource-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/datasource-icon.png" alt="" style="max-width:100%;"></a>.</li>
<li>Click <strong>Add</strong>. The New LoopBack Data Source window opens.</li>
<li>Enter <code>weatherDS</code> in the <strong>Name</strong> text field.
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
You can use any alphanumeric characters, dashes, and underscores in a data source name.</p>
</blockquote>
</li>
<li>Click <strong>New</strong>.</li>
<li>By default, the <strong>Connector</strong> setting shows <strong>In-memory db</strong> and the other settings are blank. Keep the default settings for now, and API Designer automatically saves the new data source.
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
The In-memory data source is built into LoopBack and is suitable only for development and initial testing. When you are ready to connect your models to a real data source such as a database server, change the <strong>Connector</strong> setting accordingly and install the data source connector by following the instructions in <a href="https://www.ibm.com/support/knowledgecenter/SSMNED_5.0.0/com.ibm.apic.toolkit.doc/tapim-connector-install.html#task_i2p_dnw_vv">Installing LoopBack connectors <img src="/Bluemix-Docs/apiconnect/icons/launch-glyph.svg" alt="External link icon" title="External link icon" style="max-width:100%;"></a>{:new_window}. Enter the connector settings (host name, port, database name, user name, password) as appropriate for your Connector type, and click the <strong>Save</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/save-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/save-icon.png" alt="" style="max-width:100%;"></a>. API Designer automatically tests the connection to the data source. If the test is successful, it displays the message <strong>Success - Data source connection test succeeded</strong>.</p>
</blockquote>
</li>
<li>Click the Test Connection icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/db-test-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/db-test-icon.png" alt="" style="max-width:100%;"></a> to test the data source connection. The message "Data source connection test succeeded" is displayed.</li>
<li>Click <strong>All Data Sources</strong>. The data source will appear in the list of data sources, and the editor updates the server/datasources.json file with settings for the new data source.</li>
</ol>
<h3><a id="user-content-add-a-model" class="anchor" href="#add-a-model" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add a model</h3>
<p>To add a new model to a LoopBack project using the API Designer, complete the following steps:</p>
<ol>
<li>Click the <strong>Models</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/models-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/models-icon.png" alt="" style="max-width:100%;"></a>.</li>
<li>Click <strong>Add</strong>. The New LoopBack Model window opens.</li>
<li>Enter <code>weather</code> in the <strong>Name</strong> text field, then click <strong>New</strong>.</li>
<li>In the <strong>Data Source</strong> field, select <strong>weatherDS</strong>.
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/new-model-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/new-model-1.png" alt="" style="max-width:100%;"></a></li>
<li>In the <strong>Properties</strong>, click the <strong>Add property</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/add-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/add-icon.png" alt="" style="max-width:100%;"></a>.</li>
<li>In the <strong>Property Name</strong> text field, enter <code>zip_code</code>.</li>
<li>For <strong>Type</strong>, select <strong>number</strong>.</li>
<li>Select <strong>Required</strong> to make the property required. This means that it must have a value when you add or update a model instance. For now, keep the default values for the other settings:
<ul>
<li><strong>Is Array</strong>: Whether the property is a JavaScript array with elements of the specified type.</li>
<li><strong>ID</strong>: Whether the property is a unique identifier.</li>
<li><strong>Index</strong>: Whether the property represents a column (field) that is a database index.</li>
<li><strong>Description</strong>: Text description of the property.</li>
</ul>
</li>
<li>Click the <strong>Add property</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/add-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/add-icon.png" alt="" style="max-width:100%;"></a> again to add another property.  Reference the table below to complete the remaining properties:
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/new-model-property-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/new-model-property-1.png" alt="" style="max-width:100%;"></a></li>
<li>Click the <strong>Save</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/save-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/save-icon.png" alt="" style="max-width:100%;"></a> to save your changes.</li>
<li>Click <strong>All Models</strong> to finish editing the model.</li>
</ol>
<p>This completes adding a new data source and model to the weather-data LoopBack project.</p>
<hr>
<h2><a id="user-content-test-your-loopback-project" class="anchor" href="#test-your-loopback-project" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Test your LoopBack project</h2>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
&gt;You can go directly to step 2 below if you did not exit {{site.data.keyword.apiconnect_short}} designer after completing the "Add a new model and data source" section.</p>
</blockquote>
<p>To test your API endpoints using the API Designer Explore tool, complete the following steps:</p>
<ol>
<li>
<p>From the command line, enter the following command:</p>
<div class="highlight highlight-source-shell"><pre>apic edit</pre></div>
<p>After a brief pause, the console displays this message:</p>
<div class="highlight highlight-source-shell"><pre>Express server listening on http://127.0.0.1:9000</pre></div>
<p>The API Designer opens in your default web browser, initially displaying the login page if you haven't logged in recently.</p>
</li>
<li>
<p>Start the local test servers.
a. In the test console at the bottom of the screen, click the <strong>Start the servers</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/test-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/test-icon.png" alt="" style="max-width:100%;"></a>:
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/start-server-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/start-server-1.png" alt="" style="max-width:100%;"></a>
b. Wait until the Running message is displayed:
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/running-server-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/running-server-1.png" alt="" style="max-width:100%;"></a></p>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
Depending on your project configuration and whether other processes are running, different port numbers might be displayed.</p>
</blockquote>
</li>
<li>
<p>Click <strong><a href="http://127.0.0.1:port_number">http://127.0.0.1:port_number</a></strong> to display the API root endpoint. For the default LoopBack (empty or hello-world) project, you'll see something like this:</p>
<div class="highlight highlight-source-shell"><pre>{<span class="pl-s"><span class="pl-pds">"</span>started<span class="pl-pds">"</span></span>:<span class="pl-s"><span class="pl-pds">"</span>2017-05-24T19:21:47.807Z<span class="pl-pds">"</span></span>,<span class="pl-s"><span class="pl-pds">"</span>uptime<span class="pl-pds">"</span></span>:80.876}</pre></div>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/info.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/info.png" alt="info" title="Information" style="max-width:100%;"></a>
To stop your project, click the <strong>Stop the servers</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/stop-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/stop-icon.png" alt="" style="max-width:100%;"></a>:
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/stop-server-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/stop-server-1.png" alt="" style="max-width:100%;"></a></p>
</blockquote>
<blockquote>
<p>To restart it, click the <strong>Restart the servers</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/restart-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/restart-icon.png" alt="" style="max-width:100%;"></a>:
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/restart-server-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/restart-server-1.png" alt="" style="max-width:100%;"></a></p>
</blockquote>
</li>
<li>
<p>Click the <strong>Explore</strong> icon <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/explore-icon.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/explore-icon.png" alt="" style="max-width:100%;"></a> to see the API Designer Explore tool. The sidebar shows all of the REST operations for the LoopBack models in the API. Models that are based on PersistedModel by default have a <a href="http://loopback.io/doc/en/lb2/PersistedModel-REST-API">standard set of create, read, update, and delete operations <img src="/Bluemix-Docs/apiconnect/icons/launch-glyph.svg" alt="External link icon" title="External link icon" style="max-width:100%;"></a>{:new_window}.</p>
</li>
<li>
<p>Click the operation <strong>weather.create</strong> in the left pane to display the endpoint.
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/explore-test-1.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/explore-test-1.png" alt="" style="max-width:100%;"></a>
The center pane displays summary information about the endpoint, including its parameters, security, model instance data, and response codes. The right pane provides template code to call the endpoint using the curl command, and languages such as Ruby, Python, Java, and Node.</p>
</li>
<li>
<p>To test the REST endpoints in the API Designer Explore tool, on the right pane click <strong>Try it</strong>. Scroll down to <strong>Parameters</strong> and click <strong>Generate</strong> to generate some dummy data. By default, the generated data includes the <code>zip_code</code>, <code>current_temperature</code>, <code>current_humidity</code>, <code>tonight_temperature_low</code>, <code>tonight_temperature_high</code>, <code>tonight_humidity_low</code>, <code>tonight_humidity_high</code> and <code>id</code> properties.
<em>Note: The <code>id</code> property is created by LoopBack for a given model and the value is automatically generated. Remove the <code>id</code> property from the sample data, update the generated data as required, and click <strong>Call operation</strong>.</em>
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/explore-test-2.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/explore-test-2.png" alt="" style="max-width:100%;"></a></p>
</li>
</ol>
<blockquote>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/troubleshooting.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/troubleshooting.png" alt="troubleshooting" title="Troubleshooting" style="max-width:100%;"></a>
If you see an error message due to an untrusted certificate for localhost, click the link provided in the error message in API Designer Explore tool to accept the certificate, then proceed to call the operations in your web browser. The exact procedure depends on the web browser you are using. If you load the REST endpoints directly in your browser, you will see the message: {"name":"PreFlowError","message":"unable to process the request"}. You must use the API Designer Explore tool to test REST endpoints in your browser because it includes the requisite headers and other request parameters.</p>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/troubleshooting.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/troubleshooting.png" alt="troubleshooting" title="Troubleshooting" style="max-width:100%;"></a>
If you get a response code of <strong>422 - Unprocessable Entity</strong> with the following payload:
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/explore-test-3.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/explore-test-3.png" alt="" style="max-width:100%;"></a></p>
<p>the <code>id</code> data element has not been removed from the generated data. Remove the <code>id</code> data element and re-run the test.
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/troubleshooting.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/troubleshooting.png" alt="troubleshooting" title="Troubleshooting" style="max-width:100%;"></a>
If you get the error <strong>failed to parse request body</strong>, you have to remove the comma following the last <code>humidity_high</code> number.</p>
</blockquote>
<ol start="7">
<li>
<p>Edit the values in the JSON shown in the <strong>data</strong> section. Try changing the generated dummy data, and click <strong>Call operation</strong> again. You should see the request and response parameters, along with the JSON instance data that you entered.
<a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/explore-test-4.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/explore-test-4.png" alt="" style="max-width:100%;"></a></p>
</li>
<li>
<p>To confirm that the operation added a model instance, click <strong>weather.find</strong>. Click <strong>Call operation</strong> to display all weather instances. For example (with two model instances):</p>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/images/explore-test-5.png" target="_blank"><img src="/Bluemix-Docs/apiconnect/raw/staging/tutorials/images/explore-test-5.png" alt="" style="max-width:100%;"></a></p>
</li>
</ol>
<hr>
<h3><a id="user-content-what-you-accomplished-in-this-tutorial" class="anchor" href="#what-you-accomplished-in-this-tutorial" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>What you accomplished in this tutorial</h3>
<p>In this tutorial, you completed the following:</p>
<ol>
<li>Created a new LoopBack project using the {{site.data.keyword.apiconnect_short}} toolkit command line.</li>
<li>Added a new model and data source to a LoopBack project by using the API Designer in {{site.data.keyword.apiconnect_short}} toolkit.</li>
<li>Tested your API endpoints by using the API Designer Explore tool.</li>
</ol>
<hr>
<h2><a id="user-content-next-step" class="anchor" href="#next-step" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Next step</h2>
<p><a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/tut_rest_landing.html">Manage a REST service</a> or <a href="/Bluemix-Docs/apiconnect/blob/staging/tutorials/tut_manage_soap_api.html">Manage a SOAP service</a>.</p>
<p>Create &gt; <strong>Manage</strong> &gt; Secure &gt; Socialize &gt; Analyze</p>
</article>
  </div>

</div>

<button type="button" data-facebox="#jump-to-line" data-facebox-class="linejump" data-hotkey="l" class="d-none">Jump to Line</button>
<div id="jump-to-line" style="display:none">
  <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="" class="js-jump-to-line-form" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <input class="form-control linejump-input js-jump-to-line-field" type="text" placeholder="Jump to line&hellip;" aria-label="Jump to line" autofocus>
    <button type="submit" class="btn">Go</button>
</form></div>


  </div>
  <div class="modal-backdrop js-touch-events"></div>
</div>

    </div>
  </div>

  </div>

      <div class="container site-footer-container">
  <div class="site-footer" role="contentinfo">
    <ul class="site-footer-links float-right">
      <li><a href="https://developer.github.com/enterprise/2.10" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li><a href="https://training.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
      <li><a href="https://shop.github.com" data-ga-click="Footer, go to shop, text:shop">Shop</a></li>
        <li><a href="https://github.com/blog">Blog</a></li>
        <li><a href="https://github.com/about">About</a></li>

    </ul>

    <a href="https://github.ibm.com" aria-label="Homepage" class="site-footer-mark" title="GitHub Enterprise Version 2.10.10">
      <svg aria-hidden="true" class="octicon octicon-mark-github" height="24" version="1.1" viewBox="0 0 16 16" width="24"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
</a>
    <ul class="site-footer-links">
      <li>&copy; 2017 <span title="0.18126s from ghe-web-jonsnow">GitHub</span>, Inc.</li>
        <li><a href="https://help.github.com/enterprise/2.10">Help</a></li>
        <li><a href="mailto:admin@github.ibm.com">Support</a></li>
    </ul>
  </div>
</div>



  

  <div id="ajax-error-message" class="ajax-error-message flash flash-error">
    <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"/></svg>
    <button type="button" class="flash-close js-flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
      <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
    </button>
    You can't perform that action at this time.
  </div>


    
    <script crossorigin="anonymous" integrity="sha256-Hsbbc3Dg+0pE0QM5qriIFdSxsEj5anewj15xZq5kRJY=" src="https://assets.github.ibm.com/assets/frameworks-1ec6db7370e0fb4a44d10339aab88815d4b1b048f96a77b08f5e7166ae644496.js"></script>
    <script async="async" crossorigin="anonymous" integrity="sha256-vCTzJE3lOo0Q4SPYdllNVBZQyqfUkTvEb1nPjLDytO0=" src="https://assets.github.ibm.com/assets/github-bc24f3244de53a8d10e123d876594d541650caa7d4913bc46f59cf8cb0f2b4ed.js"></script>
    
    
    
    
  <div class="js-stale-session-flash stale-session-flash flash flash-warn flash-banner d-none">
    <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"/></svg>
    <span class="signed-in-tab-flash">You signed in with another tab or window. <a href="">Reload</a> to refresh your session.</span>
    <span class="signed-out-tab-flash">You signed out in another tab or window. <a href="">Reload</a> to refresh your session.</span>
  </div>
  <div class="facebox" id="facebox" style="display:none;">
  <div class="facebox-popup">
    <div class="facebox-content" role="dialog" aria-labelledby="facebox-header" aria-describedby="facebox-description">
    </div>
    <button type="button" class="facebox-close js-facebox-close" aria-label="Close modal">
      <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
    </button>
  </div>
</div>


  </body>
</html>

