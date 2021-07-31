
https://github.com/zurda/Github-Info

getinfo.js

```
class GetInfo extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: "octocat",
      user: null,
      repos: null,
      languages: null,
      maxLanguage: null,
      isInvalid: false,
      isFound: true,
      isForbidden:false,
      searchHistory: [],
      alreadyDisplayed: false
    };
    this.getInfo = this.getInfo.bind(this);
    this.getLanguages = this.getLanguages.bind(this);
    this.inputHandler = this.inputHandler.bind(this);
  }

  componentDidMount() {
    this.getInfo();
  }

getInfo() {
    const username = this.state.input;
    // check if user is already displayed
    if (this.state.user && username === this.state.user.login) {
      this.setState({
        alreadyDisplayed: true
      });
      return;
    }
        // Get user data
    const userUrl = "https://api.github.com/users/" + username + params;
    const reposUrl =
      "https://api.github.com/users/" +
      username +
      "/repos" +
      params +
      "&per_page=100";
      
          axios
      .all([axios.get(userUrl), axios.get(reposUrl)])
      .then(
        axios.spread((userResp, reposResp) => {
          this.appendToSearchHistory(userResp.data.login);

          this.setState({
            user: userResp.data,
            repos: reposResp.data,
            isFound: true,
            isForbidden:false
          });
          
  //some code to get languages, find top language and render
  
return (
      <div className="wrapper">
        <Header
          change={this.inputHandler}
          click={this.getInfo}
          searchHistory={this.state.searchHistory}
        />
        <Content
          isInvalid={this.state.isInvalid}
          isFound={this.state.isFound}
          isForbidden={this.state.isForbidden}
          user={this.state.user}
          alreadyDisplayed={this.state.alreadyDisplayed}
          handleAlreadyDisplayed={this.handleAlreadyDisplayed.bind(this)}
          repos={this.state.repos}
          topLang={topLang}
        />
        <Footer />
```
-----

displayrepos.js
```
const displayRepos = (props) => {
	let stargazers_total, 
	forks_total,
	most_starred, 
	most_forked;
	const repos = props.repos;
	if (!repos) {
		return null;
	} else {
		stargazers_total = repos.reduce( (prev,next) => prev + next.stargazers_count, 0);
		forks_total = repos.reduce( (prev,next) => prev + next.forks_count, 0);
		if (stargazers_total > 0) {
			most_starred = repos.reduce( (prev, next) =>  prev.stargazers_count > next.stargazers_count ? prev : next ); 
		}
		if (forks_total > 0) {
			most_forked = repos.reduce( (prev, next) =>  prev.forks_count > next.forks_count ? prev : next );
		}
	}
  ```
-----

displayuser.js
```
export function addCommas(str){
	return str.replace(/\B(?=(\d{3})+(?!\d))/g, ',');
}

const displayUser = ({ user, handleOnLoad }) => {
	const { login, avatar_url, name, bio, blog, location, followers, following, public_repos, hireable } = user;
	return (
		<div className='DisplayUser'>
			<a href={'https://github.com/' + login} target='_blank' >
				<img className='avatar' onLoad={handleOnLoad} src={avatar_url} alt='User profile avatar' />
			</a>
			<ValidatedField value={name} tag="h2"/>
			<p>{login}</p>
			<ValidatedField value={bio}/>
			<ValidatedField value={location}/>
			{hireable && <p>Available for job offers</p>}
			{blog && <a href={blog} target="_BLANK">{blog}</a>}
			<ValidatedField fieldName="Public Repos" value={addCommas(public_repos.toString())}/>
			<ValidatedField fieldName="Followers" value={addCommas(followers.toString())}/>
			<ValidatedField fieldName="Following" value={addCommas(following.toString())}/>
		</div>
	);
}

export default displayUser;
```
