'''
const App = () => {
  const githubState = useContext(GithubContext);
  const { searchAllUsers } = githubState;

  useEffect(() => {
    searchAllUsers();
    // eslint-disable-next-line
  }, []);
  '''
