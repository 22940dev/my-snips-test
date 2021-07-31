
https://github.com/zurda/Github-Info

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
