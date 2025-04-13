# Eat with me
 
ive indicate the code created below for my app:

package com.example.eatwithme

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.CornerSize
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.unit.dp
import androidx.compose.ui.Alignment // <-- Add this import
import com.example.eatwithme.R

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            var timeOfDay by remember { mutableStateOf("") }
            var mealSuggestion by remember { mutableStateOf("") }

            // Box to layer content
            Box(
                modifier = Modifier
                    .fillMaxSize()
            ) {
                // Background image
                Image(
                    painter = painterResource(id = R.drawable.happyfood1), // Use your image from res/drawable
                    contentDescription = "Backound Image",
                    modifier = Modifier.fillMaxSize(),
                    contentScale = ContentScale.Crop // Ensures the image covers the screen
                )

                // UI content centered on top of the image
                Column(
                    modifier = Modifier
                        .fillMaxSize()
                        .padding(30.dp)
                        .wrapContentSize(Alignment.Center), // Centers the content
                    verticalArrangement = Arrangement.Center,
                    horizontalAlignment = Alignment.CenterHorizontally // Centers the content horizontally
                ) {
                    // Header text
                    Text(
                        text = "EAT WITH ME",
                        style = MaterialTheme.typography.headlineMedium,
                        color = Color.Red // Ensure text is visible on dark backgrounds
                    )

                    Spacer(modifier = Modifier.height(20.dp))

                    // Input field for time of day
                    OutlinedTextField(
                        value = timeOfDay,
                        onValueChange = { timeOfDay = it },
                        placeholder = { Text("ADD THE TIME OF DAY") },
                        label = { Text("Time of Day") },
                        singleLine = true,
                        modifier = Modifier.fillMaxWidth()
                    )

                    Spacer(modifier = Modifier.height(16.dp))

                    // Row with buttons
                    Row(
                        horizontalArrangement = Arrangement.spacedBy(8.dp),
                        modifier = Modifier.fillMaxWidth(),
                        verticalAlignment = Alignment.CenterVertically
                    ) {
                        // Suggest button
                        Button(onClick = {
                            mealSuggestion = when (timeOfDay.lowercase()) {
                                "morning" -> "Bacon and eggs with avo on rye toast and black coffee"
                                "afternoon" -> "Grilled chicken with salad and chips with berry ice tea"
                                "evening" -> "Spicey Spaghetti bolognese meat with garlic cheese bread and red wine"
                                "night" -> "A rack of ribs and chips with coke"
                                else -> "Sorry, PLEASE TRY morning,afternoon or night !"
                            }
                        }) {
                            Text("SUGGEST")
                        }

                        // Reset button
                        Button(onClick = {
                            timeOfDay = ""
                            mealSuggestion = ""
                        }) {
                            Text("RESET")
                        }
                    }

                    Spacer(modifier = Modifier.height(16.dp))

                    // Displaying meal suggestion
                    if (mealSuggestion.isNotEmpty()) {
                        Text(
                            text = "Meal for $timeOfDay:",
                            color = Color.Black
                        )
                        Text(
                            text = mealSuggestion,
                            color = Color.Black
                        )
                    }
                }
            }
        }
    }
}
