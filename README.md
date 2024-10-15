# Intrepid
RestAssured

//import org.openqa.selenium.remote.Response;
import io.restassured.RestAssured;
import io.restassured.response.Response;
//import org.junit.jupiter.api.Test;
import org.testng.annotations.Test;
//import org.testng.Assert;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class Main {

    public Response getTodoById(int todoId){
        String url = "https://jsonplaceholder.typicode.com/todos/"+ todoId;
        return RestAssured.get(url);
    }


    @Test
    public void testGetRequestValidate(){
        String expectedTitle = "delectus aut autem";
        int expectedUserId = 1;
        int todoId = 1;
        Response response = getTodoById(todoId);
        boolean expectedCompleted = false;

        //Response response = RestAssured.get("https://jsonplaceholder.typicode.com/todos/1");
        assertEquals(200, response.getStatusCode(),"Status Code is not as expected");

        int actualUserId = response.jsonPath().getInt("userId");
        int actualId = response.jsonPath().getInt("id");
        String actualTitle = response.jsonPath().getString("title");
        boolean actualComplted = response.jsonPath().getBoolean("completed");

        assertEquals(expectedUserId, actualUserId,"User Id does not match");
        assertEquals(todoId, actualId," Id does not match");
        assertEquals(expectedTitle, actualTitle,"Title does not match");
        assertEquals(expectedCompleted, actualComplted,"Completed status does not match");

    }


}

