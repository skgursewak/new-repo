# new-repo
pm.test("Response status code is 200", function () {
    pm.response.to.have.status(200);
});


pm.test("Response time is less than 200ms", function () {
  pm.expect(pm.response.responseTime).to.be.below(200);
});


pm.test("Owner object should exist and be an object", function () {
  const responseData = pm.response.json();
  
  pm.expect(responseData).to.be.an('object');
  pm.expect(responseData.owner).to.exist.and.to.be.an('object');
});


pm.test("Topics array should be present and empty", function () {
    const responseData = pm.response.json();
    
    pm.expect(responseData).to.be.an('object');
    pm.expect(responseData.topics).to.be.an('array').that.is.empty;
});


pm.test("Languages URL should be null or a valid URL", function () {
    const responseData = pm.response.json();
    
    pm.expect(responseData).to.be.an('object');
    pm.expect(responseData.languages_url).to.satisfy((url) => {
        return url === null || url.match(/^https?:\/\/\S+/);
    }, "Languages URL should be null or a valid URL");
});
