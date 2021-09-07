# Divya Reddy Vanipanta

### My favourite location in the world is Paris

**Paris** is one of the most beautiful cities in the world. People call Paris "City of Love" because of the romatic atmosphere and **Eiffel tower** is one of the world's most recognizable landmarks.

Especially as it glows after dark have made it one of the most visited monuments in the world. Also **Paris** is a nation of food lovers, all these put together made me like Paris

***

### Route from Maryville to Overland Park, Kansas City
1.  Start from Horizon west, Maryville and head west on W 11th St toward N College Dr.
    1. Turn left onto N College Dr then turn left onto W 9th St.
    2. Turn right onto US-71 BUS S/N Main st and continue for 2.5 miles
    3. Take the ramp to US-71 S and continue for 30 miles.
1.  Now use the left lane to take the I-29 S/US-71 S exit toward US-59 S/Kansas city.
2.  Merge onto I-29 S/US-71 S and keep left at the fork to continue on i-29 S
3.  Use the right 2 lanes to take exit 3B for I-635 S toward Kansas
4.  Use the middle 2 lanes to stay on I-635 S and keep right to stay on I-635 S
5.  Continue onto US-69 S and turn right onto W 80th St and then turn left onto Overland Park Dr.
6.  Turn left and you have reached your destination.
1.  Items to be bought to Overland Park
    1.  Music System
    1.  Indoor Games
    1.  Movies

**[Learn about me here](AboutMe.md)**

***

### Food/Drinks Recommendations

The below table contains the list of **Food and Bevarages** one can try. It also contains the location where you can get the Item and the estimated price of Item

| Food/Beverage | Locaiton | Estimated Price |
| ------------- | -------- | --------------- |
| Biryani | Overland Park | $12.99 |
| Apple Pie | New Mexico | $9.83 |
| Tacos | Los Angeles | $2.19 |
| The Hamburger | New Haven | $4.56 |
| Pisco Sour | New York | $4.00 |

***

### Inspirational Quotes

> "It doesn't matter who you are, where you come from. The ability to triumph begins with you." -*Oprah Winfrey*

> "Believe you can and you're halfway there." -*Theordore Roosevelt*

> "The only person you are destined to become is the person you decide to be." -*Ralph Waldo Emerson*

***

### Convex Hull construction using Graham's Scan

> Graham's scan is a method of finding the convex hull of a finite set of points in the plane with time complexity O(n log n). It is named after Ronald Graham, who published the original algorithm in 1972. The algorithm finds all vertices of the convex hull ordered along its boundary. It uses a stack to detect and remove concavities in the boundary efficiently.

*Convex Hull construction* description: <https://en.wikipedia.org/wiki/Graham_scan>

```
struct pt {
    double x, y;
};

bool cmp(pt a, pt b) {
    return a.x < b.x || (a.x == b.x && a.y < b.y);
}

bool cw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) < 0;
}

bool ccw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) > 0;
}

void convex_hull(vector<pt>& a) {
    if (a.size() == 1)
        return;

    sort(a.begin(), a.end(), &cmp);
    pt p1 = a[0], p2 = a.back();
    vector<pt> up, down;
    up.push_back(p1);
    down.push_back(p1);
    for (int i = 1; i < (int)a.size(); i++) {
        if (i == a.size() - 1 || cw(p1, a[i], p2)) {
            while (up.size() >= 2 && !cw(up[up.size()-2], up[up.size()-1], a[i]))
                up.pop_back();
            up.push_back(a[i]);
        }
        if (i == a.size() - 1 || ccw(p1, a[i], p2)) {
            while(down.size() >= 2 && !ccw(down[down.size()-2], down[down.size()-1], a[i]))
                down.pop_back();
            down.push_back(a[i]);
        }
    }

    a.clear();
    for (int i = 0; i < (int)up.size(); i++)
        a.push_back(up[i]);
    for (int i = down.size() - 2; i > 0; i--)
        a.push_back(down[i]);
}
```

*Convex Hull construction* Code Source: <https://cp-algorithms.com/geometry/grahams-scan-convex-hull.html>