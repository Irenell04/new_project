import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:flutter/material.dart';

class RestaurantList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return StreamBuilder(
      stream: FirebaseFirestore.instance.collection('restaurants').snapshots(),
      builder: (context, AsyncSnapshot<QuerySnapshot> snapshot) {
        if (!snapshot.hasData) return CircularProgressIndicator();
        return ListView.builder(
          itemCount: snapshot.data!.docs.length,
          itemBuilder: (context, index) {
            var restaurant = snapshot.data!.docs[index];
            return ListTile(
              title: Text(restaurant['name']),
              subtitle: Text(restaurant['cuisine']),
              leading: Image.network(restaurant['imageUrl']),
            );
          },
        );
      },
    );
  }
}
